# t5-large

T5(Text-to-Text Transfer Transformer)由谷歌的 Raffel 等人于 2020年7月提出，该模型将翻译、分类、回归、摘要生成等任务都统一转成`Text-to-Text`任务，从而使得这些任务在训练(pre-train和fine-tune)时能够使用相同的目标函数，在测试时也能使用相同的解码过程。

T5-large模型包含739M参数。

参考：[https://arxiv.org/abs/1910.10683](https://arxiv.org/abs/1910.10683)
