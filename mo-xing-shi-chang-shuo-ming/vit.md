# ViT

自2017年Google提出的Transformer结构以来，迅速引发一波热潮，最初《Attention is all you need》这篇论文的提出是针对于NLP领域的，通过自注意力机制代替传统处理序列数据时采用的循环神经网络结构，不仅实现了并行训练，提升了训练的效率，同时也在应用中取得很好的结果。之后的一段时间中，各种基于Transformer改进的网络结构涌现出来，在不同领域中都达到SOTA的效果。

2020年Google又提出了《AN IMAGE IS WORTH 16X16 WORDS : TRANSFORMERS FOR IMAGE RECOGNITION AT SCALE》这篇论文，该文章已经被收录于ICLR 2021。首次提出Vision Transformer(ViT)将Transformer结构应用在了CV领域图像分类中，论文中表明，与当前效果最好的卷积神经网络结构相比，ViT仍然取得很好的成绩，同时需要更少的计算资源。&#x20;

参考：https://blog.csdn.net/Yore\_/article/details/123847838
