# 基本概念

## 1. 可用区

可用区是指在同一地域内，电力和网络互相独立的物理区域，同一可用区内实例之间的网络延时更小，用户访问速度更快。

平台提供了多个可用区供用户选择，在控制台的左上角可以切换可用区。

## 2. 网盘

平台为每个用户提供了一块持久化，无限大，租户隔离的存储区域，叫做网盘。用户可以把网盘看成是一个云端U盘，可以存放任何数据。网盘默认有一个叫做data的文件夹，会默认挂载到所有的工作空间中，即该文件夹中的内容，会在多个工作空间中共享。

用户可以直接在浏览器中对网盘的文件进行操作，例如创建文件夹，上传文件，删除文件等等。 对于超过10M的大文件，建议通过命令行的方式进行上传。

网盘底层使用了分布式存储技术，提供99.9999999%的数据可靠性。

## 3. 数据盘

平台提供持久化存储的空间，叫做数据盘。数据盘的IO性能要比网盘快，和系统盘基本一致。和系统盘不同的是，工作空间停止或者重启后，数据盘的数据不会丢失，而系统的数据会丢失。

工作空间可以携带数据盘，用户可单独新建数据盘，或在创建工作空间时新建数据盘，此外创建工作空间时也可挂载已有数据盘（需要注意的是，工作空间挂载已有数据盘时，仅有数据盘类型与资源类型对应的情况可被挂载），工作空间也可将数据盘进行卸载，以便其他工作空间挂载使用。

数据盘在被销毁前会持久化存储其中的数据，对应的平台也会持续计费。对应的，数据盘销毁后会停止计费，数据盘中的数据也会被删除。

数据盘提供多种规格，用户可按需使用。

## 4. 数据集和模型

为了方便数据流通，平台提供了数据集市场和模型市场。用户可以从数据集市场/模型市场上购买数据集/模型，也可以将自己网盘中的内容发布到数据集市场/模型市场，发布数据集/模型需要等待平台审批后才能生效。

当前数据集市场/模型市场上绝大部分的数据集/模型都可限时免费使用。

## 5. 工作空间

平台提供了多个AI开发环境镜像（预置不同的机器学算法依赖和框架），用户可以购买一台按使用量计费或者包年包月计费的GPU资源，加载镜像后启动一个工作空间。工作空间内置了Jupyter和VSCode两种开发工具，支持grafana监控，事件日志，SSH登录，支持快照。

平台提供了常见的开发环境，说明如下：

<table><thead><tr><th width="153">镜像名</th><th width="116">CUDA</th><th width="108">CUDANN</th><th width="173">框架</th><th>开发工具</th></tr></thead><tbody><tr><td>pytorch</td><td>cuda11.6</td><td>cudann8</td><td>pytorch1.12.1</td><td>Jupyter, VSCode</td></tr><tr><td>pytorch</td><td>cuda11.7</td><td>cudann8</td><td>pytorch2.0</td><td>Jupyter, VSCode</td></tr><tr><td>tensorflow</td><td>cuda11.6</td><td>cudann8</td><td>tensorflow2.8.0</td><td>Jupyter, VSCode</td></tr><tr><td>other/base</td><td>cuda11.7</td><td>cudann8</td><td>-</td><td>Jupyter, VSCode</td></tr></tbody></table>

<figure><img src="../.gitbook/assets/image (73).png" alt=""><figcaption><p>查看cuda和cudann版本的命令</p></figcaption></figure>

工作空间支持使用用户自定义镜像，镜像需要先上传到平台的镜像仓库方可使用。

## 6. 推理服务

用户可以在平台创建推理服务，推理服务支持基于AKSK的认证机制，支持Auto Scaling弹性扩缩容实例，支持在线升级。

推理服务支持用户自定义镜像，并支持模型和镜像分离，从而实现灵活的动态更换模型。

## 7. 应用

平台提供多种应用，用户可以像使用PC上的应用程序或者手机上的App一样使用应用，而无需关心应用底层的实现细节和计算存储消耗。

说明：应用当前为内测阶段，后续可能会根据市场情况，调整应用及其计费模式。





