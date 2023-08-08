# ImageNet

ImageNet是大规模视觉识别挑战赛 (ILSVRC) 2012-2017 图像分类和定位数据集，因此也被称为ImageNet ILSVRC数据集。该数据集有1000 个分类，包含 1,281,167 个训练图像、50,000 个验证图像和 100,000 个测试图像。

分类任务涉及以几个文件：

* ILSVRC2012\_img\_train.tar：训练数据集，共1,281,167个图片，1000个种类，是ImageNet 的子集，其中每种类型都有732 到 1300张图片，这个文件夹下面是1000个子文件夹，每个文件夹都以WNID来命名，比如n01440764。图片都是JPEG格式，可以直接通过pytorch提供的ImageNet类来使用
* ILSVRC2012\_img\_val.tar：验证数据集，共50,000张图片，每个类型都有50张
* ILSVRC2012\_img\_test.tar：测试数据集，共有100,000张图片，每个类型有100张
* ILSVRC2012\_devkit\_t12.tar.gz：验证数据集的Ground truth





