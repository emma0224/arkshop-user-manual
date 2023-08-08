# 创建并发布一个自定义应用

**说明：自定义应用功能当前只对受邀客户开发，请联系小助手申请名额。**

平台提供自定义应用的功能，用户可以将自己的镜像封装为一个应用，方便后续的使用。您也可以将应用发布到平台的应用市场，后台审核后，其他用户就可以安装并使用您的应用了。这里我们举个例子，创建一个同态加密的应用，并发布到市场。

## 第一步：上传镜像

在控制台导航栏选择镜像-私有镜像，点击查看推送命令，将镜像推送到平台的镜像仓库。这里我们推送的镜像名为he-calc。

<figure><img src="../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

## 第二步：定义应用

在控制台导航栏选择应用，点击右上角创建应用，输入应用名称，镜像选择刚才上传的镜像，输入启动脚本，以及参数配置。这里的参数配置是在定义运行该应用时需要的参数，我们的这个例子中，需要定义三个参数：

* pubkey\_file：公钥文件，必填参数，数据类型为data，即是一个网盘的文件/文件夹，或者数据集中的文件/文件夹。
* data1\_enc\_file：加密后的向量文件1，必填参数，数据类型为data，即是一个网盘的文件/文件夹，或者数据集中的文件/文件夹。
* data2\_enc\_file：加密后的向量文件1，必填参数，数据类型为data，即是一个网盘的文件/文件夹，或者数据集中的文件/文件夹。

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

## 第三步：运行实例

应用定义完成后，会出现在应用-我创建的 tab下，点击详情进入应用详情页面。

<figure><img src="../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

因为这个应用需要三个参数，所以事先需要把这三个文件上传到网盘，一个小TIPS是，在网盘文件或者文件夹的右侧，点击复制地址，可以直接复制文件路径。

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

我们运行实例进行测试，点击新建实例，设置实例名称，填写实例参数（注意如果数据来自网盘，需要在Value里设置disk，如果来自数据集，需要在Value里设置dataset），选择资源（这里我们使用CPU资源），点击提交，稍等片刻，等待运行结果为完成。

<figure><img src="../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>



## 第四步：发布应用

在控制台-应用-我创建的tab下找到刚才创建的应用，点击右侧发布按钮，填写相关信息后，就可以提交发布。待后台审核后，该应用就会出现在平台的应用市场。

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

为了方便大家使用，我们也可以把输入需要的例子文件（即公钥pubkey，以及两个加密后的数文件）发布到数据集市场，方便大家测试使用，该例子的数据集为homomorphic-encryption。









