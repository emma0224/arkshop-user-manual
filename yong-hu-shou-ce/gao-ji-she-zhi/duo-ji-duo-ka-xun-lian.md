# 多机多卡训练

这是一个简单的多机多卡训练例子。使用两台单卡机器共同训练一个简单的minst分类模型。 我们有两台实例，分别为实例1和实例2。我们提供两个训练文件

1. 我们在平台内分别使用ifconfig命令查看本机IP地址。

```
ifconfig
eth0: flags=4291<UP,BROADCAST,RUNNING,NOARP,MULTICAST>  mtu 1500
        inet 172.29.144.98  netmask 255.255.254.0  broadcast 172.29.145.255
        ether fa:26:00:0d:b1:d4  txqueuelen 0  (Ethernet)
        RX packets 32178  bytes 2692902 (2.6 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 47038  bytes 8911706 (8.9 MB)
```

2. 将实例1的ip地址填入实例2上的init\_method，同时指定指定实例2为rank1.

```python
import torch
import torch.nn as nn
import torch.optim as optim
import torch.distributed as dist
import torchvision.datasets as datasets
import torchvision.transforms as transforms
from torch.utils.data import DataLoader
from torch.utils.data.distributed import DistributedSampler

# 设置分布式参数
world_size = 2
rank = 1
dist.init_process_group(backend='nccl', init_method='tcp://172.29.144.98:23456', world_size=world_size, rank=rank)

# 定义模型
model = nn.Sequential(nn.Linear(784, 256),
                      nn.ReLU(),
                      nn.Linear(256, 10),
                      nn.LogSoftmax(dim=1))

# 将模型放到GPU上
model.cuda()

# 定义损失函数和优化器
criterion = nn.NLLLoss()
optimizer = optim.SGD(model.parameters(), lr=0.01)

# 加载数据
train_dataset = datasets.MNIST('./data', train=True, download=True,
                               transform=transforms.Compose([
                                   transforms.ToTensor(),
                                   transforms.Normalize((0.1307,), (0.3081,))
                               ]))
train_sampler = DistributedSampler(train_dataset, num_replicas=world_size, rank=rank)
train_loader = DataLoader(train_dataset, batch_size=64, sampler=train_sampler)

# 训练模型
epochs = 100
for epoch in range(epochs):
    train_loss = 0.0
    for data, target in train_loader:
        data, target = data.cuda(), target.cuda()
        optimizer.zero_grad()
        output = model(data.view(data.shape[0], -1))
        loss = criterion(output, target)
        loss.backward()
        optimizer.step()
        train_loss += loss.item() * data.size(0)
    train_loss /= len(train_loader.sampler)
    print(f"Epoch: {epoch+1}, Train Loss: {train_loss}")

```

3. 将实例 1init\_method 指定为tcp://0.0.0.0:23456，并指定实例1为rank0

```python
import torch
import torch.nn as nn
import torch.optim as optim
import torch.distributed as dist
import torchvision.datasets as datasets
import torchvision.transforms as transforms
from torch.utils.data import DataLoader
from torch.utils.data.distributed import DistributedSampler


# 设置分布式参数
world_size = 2
rank = 0
dist.init_process_group(backend='nccl', init_method='tcp://0.0.0.0:23456', world_size=world_size, rank=rank)


# 定义模型
model = nn.Sequential(nn.Linear(784, 256),
                      nn.ReLU(),
                      nn.Linear(256, 10),
                      nn.LogSoftmax(dim=1))


# 将模型放到GPU上
model.cuda()


# 定义损失函数和优化器
criterion = nn.NLLLoss()
optimizer = optim.SGD(model.parameters(), lr=0.01)


# 加载数据
train_dataset = datasets.MNIST('./data', train=True, download=True,
                               transform=transforms.Compose([
                                   transforms.ToTensor(),
                                   transforms.Normalize((0.1307,), (0.3081,))
                               ]))
train_sampler = DistributedSampler(train_dataset, num_replicas=world_size, rank=rank)
train_loader = DataLoader(train_dataset, batch_size=64, sampler=train_sampler)


# 训练模型
epochs = 100
for epoch in range(epochs):
    train_loss = 0.0
    for data, target in train_loader:
        data, target = data.cuda(), target.cuda()
        optimizer.zero_grad()
        output = model(data.view(data.shape[0], -1))
        loss = criterion(output, target)
        loss.backward()
        optimizer.step()
        train_loss += loss.item() * data.size(0)
    train_loss /= len(train_loader.sampler)
    print(f"Epoch: {epoch+1}, Train Loss: {train_loss}")
```

4. 在两台实例上分别运行train\_rank0.py和train\_rank1.py。可以看到在建立连接后，将开始分布式训练。

<figure><img src="../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>
