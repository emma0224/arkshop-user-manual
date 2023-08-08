# 设置SSH Key

通过设置SSH Key，可以实现SSH方式免密登录到工作空间。<mark style="color:red;">注意，已经运行的工作空间，如果设置了新的SSH Key，需要停止工作空间再启动后才能生效。</mark>



## MAC/Linux 系统

### 步骤1: 检查本地SSH密钥文件

在本地机器上执行以下命令来检查是否已经有SSH密钥文件:

```bash
ls ~/.ssh
```

正确的密钥文件应包含私钥文件`id_rsa`和公钥文件`id_rsa.pub`。如果该目录不存在或文件信息不完整，执行步骤2。如果密钥信息完整，则执行步骤3。

### 步骤2: 在本地生成SSH密钥

在本地机器上执行以下命令来生成SSH密钥：

```bash
ssh-keygen -t rsa -C "your-email@example.com"
```

命令执行过程中遇到提示点击回车即可。命令执行完毕，会在`~/.ssh/`的路径下生成私钥文件`id_rsa`和公钥文件`id_rsa.pub`。你可以通过命令`ls ~/.ssh`查看。

### 步骤3: 上传SSH公钥信息

在本地机器上执行命令`cat ~/.ssh/id_rsa.pub`，复制输出的全部信息。然后点击揽睿平台右上角的头像，进入设置-ssh-key页面，点击新增key按钮，将刚刚复制的信息粘贴进去。此时您的工作空间应处于关闭状态，若您的工作空间已开启，参见临时方案。

### 步骤4: 开启工作空间

在工作空间列表中点击操作栏的更多-复制ssh命令，默认格式为`ssh user@ssh.rde-ws.lanrui-ai.com -p xxxxx -i ~/.ssh/id_rsa`。在本地运行该命令即可免密登录。若您使用的是non-official镜像，将命令修改为`ssh youkaichao@ssh.rds-ws.lanrui-ai.com -p xxxxx -i ~/.ssh/id_rsa`。

## Windows系统

以下是在Windows系统上通过命令提示符（CMD）配置SSH的步骤：

### 步骤1: 检查本地SSH密钥文件

在Windows命令提示符中，输入以下命令以检查是否存在SSH密钥文件（假设你的用户名是YourUserName）：

```cmd
dir C:\Users\YourUserName\.ssh\
```

正确的密钥文件应包含私钥文件`id_rsa`和公钥文件`id_rsa.pub`。如果该目录不存在或文件信息不完整，执行步骤2。如果密钥信息完整，则执行步骤3。

### 步骤2: 在本地生成SSH密钥

在Windows命令提示符中，输入以下命令以生成SSH密钥：

```cmd
ssh-keygen -t rsa -C "your-email@example.com"
```

命令执行过程中遇到提示点击回车即可。命令执行完毕，会在`C:\Users\YourUserName\.ssh\`的路径下生成私钥文件`id_rsa`和公钥文件`id_rsa.pub`。你可以通过命令`dir C:\Users\YourUserName\.ssh\`查看。

### 步骤3: 上传SSH公钥信息

在命令提示符中，输入命令`type C:\Users\YourUserName\.ssh\id_rsa.pub`，复制输出的全部信息。然后点击揽睿平台右上角的头像，进入设置-ssh-key页面，点击新增key按钮，将刚刚复制的信息粘贴进去。此时您的工作空间应处于关闭状态，若您的工作空间已开启，参见临时方案。

### 步骤4: 开启工作空间

在工作空间列表中点击操作栏的更多-复制ssh命令，默认格式为`ssh user@ssh.rde-ws.lanrui-ai.com -p xxxxx -i C:\Users\YourUserName\.ssh\id_rsa`。在本地运行该命令即可免密登录。若您使用的是non-official镜像，将命令修改为`ssh youkaichao@ssh.rds-ws.lanrui-ai.com -p xxxxx -i C:\Users\YourUserName\.ssh\id_rsa`。

## 临时方案

工作空间开启后，无法更新您所需的ssh密钥信息，我们提供两种方案供您选择。

### 方案1

关闭工作空间，再开启。之后您可以直接使用我们提供命令免密登陆。注意：关机后开机会重新开始计费。

### 方案2

1. 打开jupyter或code-server并进入工作空间。
2. 打开一个新的命令行窗口或者终端。
3.  输入以下命令，它会输出工作空间的私钥信息：

    ```bash
    cat ~/.ssh/id_rsa
    ```
4. 复制输出的私钥信息。
5. 在您的本地机器上打开一个新的命令行窗口或终端。
6.  输入以下命令，将工作空间的私钥信息复制并保存到您本地机器的指定路径。您可以自定义保存路径，这里以`~/workspace-ssh/`为例：

    ```bash
    echo '工作空间的私钥信息' > ~/workspace-ssh/id_rsa
    ```

    请记住将'工作空间的私钥信息'替换为步骤4中复制的私钥信息。
7.  输入以下命令，修改保存的私钥文件的权限，使其仅对您的用户帐户可读：

    ```bash
    chmod 0600 ~/workspace-ssh/id_rsa
    ```
8.  现在，您可以在SSH登录命令中使用 `-i` 参数指定私钥文件，例如：

    ```bash
    ssh user@ssh.rde-ws.lanrui-ai.com -p xxxxx -i ~/workspace-ssh/id_rsa
    ```

    在这个命令中，`user`是您的用户名，`ssh.rde-ws.lanrui-ai.com`是服务器地址，`xxxxx`是端口号，`~/workspace-ssh/id_rsa`是私钥文件的路径。
9. 在您的本地机器上执行上述命令，您就可以免密登录了。

注意：这个方法无需执行关机再开机，所以不会重新计费。
