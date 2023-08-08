# 无代码构建一个网页游戏

使用平台的推理功能，可以无代码的构建一个网页游戏，下面以2048这个游戏为例进行说明：

第一步：从github上[下载](https://github.com/gabrielecirulli/2048)该游戏，并上传到网盘。为了方便起，我们也上传到了公共模型game-2048

第二步：点击控制台-推理服务-创建推理服务，资源选择2C4G的CPU机型即可。在推理服务的配置页面，选择镜像为公共镜像-other-nginx，端口80，启动脚本为：nginx -g "daemon off;"，模型位置选择从网盘（选择刚才上传的代码路径）或者从模型（选择模型game-2048）挂载路径填写/usr/share/nginx/html/，点击高级配置，运行用户ID改成0，并关闭认证，点击创建实例。

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

第三步：在推理服务详情中，复制推理服务的请求地址，用浏览器打开即可。

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>
