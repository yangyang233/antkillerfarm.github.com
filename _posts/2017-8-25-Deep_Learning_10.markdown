---
layout: post
title:  深度学习（十）——花式卷积
category: DL 
---

# 并行 & 框架（续）

https://mp.weixin.qq.com/s/irvBbPKENiZX9G_6wh5c-Q

陈天奇等人提出TVM：深度学习自动优化代码生成器

https://mp.weixin.qq.com/s/28n8g_epHsYB0I9GVc_lww

陈天奇团队TVM重磅更新：直接在浏览器使用GPU

https://mp.weixin.qq.com/s/UxN9ZRmKLN30s7uPqMpHPQ

Jeff Dean等提出动态控制流编程模型，大规模机器学习性能提升21%

https://mp.weixin.qq.com/s/fx0Pfu0MOPjSkzi5mL6U_A

清华&斯坦福提出深度梯度压缩DGC，大幅降低分布式训练网络带宽需求

https://mp.weixin.qq.com/s/wIdTDHEPffWqHA3_XWBLyw

没错，纯SQL查询语句可以实现神经网络。

>SQL跑神经网络固然没有太大意义，然而分布式数据库已经有数十年的历史，对于设计分布式深度学习框架亦有重大的启发意义。

https://zhuanlan.zhihu.com/p/33351291

基于忆阻器（ReRAM），Computing-in-Memory的DLA

https://mp.weixin.qq.com/s/eTwSo3GnxSnK-BwwZeWmKA

Jeff Dean等提出自动化分层模型，优化CPU、GPU等异构环境，性能提升超60%

https://mp.weixin.qq.com/s/q0VENBNgolpeWmDapF5q_g

在有池化层、1步幅的CNN上减少冗余计算，一种广泛适用的架构转换方法

https://mp.weixin.qq.com/s/sn8fMAbJbeT6JUbCpBpN6A

Jeff Dean与David Patterson：不思考体系结构的深度学习研究者不是好工程师

https://mp.weixin.qq.com/s/6zLrWJ4nE0bHFlVe5dMxHw

分布式深度学习新进展：让“分布式”和“深度学习”真正深度融合

https://mp.weixin.qq.com/s/hjC-WTMIpbWWpmXoLBfD2g

腾讯大规模分布式机器学习系统无量是如何进行技术选型的？

https://mp.weixin.qq.com/s/mg-d1W5i9rzaLMNrvq0tSQ

32分钟训练神经机器翻译，速度提升45倍

https://mp.weixin.qq.com/s/iW0k80TUPuWDE9xwHvX91g

为什么你需要Raven：全球首个真正分布式深度学习训练协议

https://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650750181&idx=1&sn=156dac3c5646143fc2577972f1506836

GPU捉襟见肘还想训练大批量模型？谁说不可以

https://mp.weixin.qq.com/s/UbZtUL6Iveb4S3nTU0liGw

深度神经网络的分布式训练概述：常用方法和技巧全面总结

https://mp.weixin.qq.com/s/kLXJsHbBnRIFC3NLChPhzA

如何高效进行大规模分类？港中文联合商汤提出新方法

https://mp.weixin.qq.com/s/F10UaaoxGPOE4pc59LBCRw

数据并行化对神经网络训练有何影响？谷歌大脑进行了实证研究

https://mp.weixin.qq.com/s/UF7DDenUQJ3bL83IHxOkIw

分布式优化算法及其在多智能体系统与机器学习中的应用

https://mp.weixin.qq.com/s/6h9MeBs89hTtWsYSZ4pZ5g

蚂蚁金服核心技术：百亿特征实时推荐算法揭秘

https://mp.weixin.qq.com/s/xV5cLbCPb7Nh6i4i7DxJIQ

没人告诉你的大规模部署AI高效流程！

https://mp.weixin.qq.com/s/8R7YhcZ_Dt0oFIF3bQovxw

为了提升DL模型性能，阿里工程师打造了流式编程框架

https://mp.weixin.qq.com/s/z6gXp-EeDID1ed8_DsUbOg

90秒训练AlexNet！商汤刷新纪录

https://mp.weixin.qq.com/s/HY2yPZ--Zm5_m3B70baWjQ

谷歌开源效率怪兽GPipe，速度提升25倍，CIFAR-10精度达到99%

https://mp.weixin.qq.com/s/HQW2bPyDY_3ecZWP6NYr-w

大规模机器学习在LinkedIn预测模型中的应用实践

https://mp.weixin.qq.com/s/i1PLA1xr3CefKx1EcVUVIg

谷歌破世界纪录！圆周率计算到小数点后31.4万亿位

https://mp.weixin.qq.com/s/rX8L63-jDGJT6lCAj04I3Q

独家解读！阿里重磅发布机器学习平台PAI 3.0

# 花式卷积

在DL中，卷积实际上是一大类计算的总称。除了原始的卷积、反卷积（Deconvolution）之外，还有各种各样的花式卷积。

## 卷积在CNN和数学领域中的概念差异

首先需要明确一点，CNN中的卷积和反卷积，实际上和数学意义上的卷积、反卷积是有差异的。

数学上的**卷积**主要用于傅立叶变换，在计算的过程中，有一个时域上的反向操作，并不是简单的向量内积运算。在信号处理领域，卷积主要用作**信号的采样**。

数学上的**反卷积**主要作为卷积的逆运算，相当于**信号的重建**，或者解微分方程。因此，它的难度远远大于卷积运算，常见的有Wiener deconvolution、Richardson–Lucy deconvolution等。

CNN的反卷积就简单多了，它只是误差的反向算法而已。因此，也有人用back convolution, transpose convolution, Fractionally Strided Convolution这样更精确的说法，来描述CNN的误差反向算法。

## Deconvolution

在《深度学习（三）》中，我们已经给出了Deconvolution的推导公式，但是并不直观。这里补充说明一下。

![](/images/article/no_padding_strides_transposed.gif)

上图是transpose convolution的操作。或者也可以看下图：

![](/images/img2/deconv.png)

上面的图主要是直观理解。实际计算中，除了使用GEMM之外，更常见的方法不是input padding，而是采用下图的办法：

![](/images/img2/deconv.jpg)

这个方法的步骤如下：

1.kernel padding。把[2, 2, Input, Output]的kernel，pad成[1, 1, Input, Output x 4]。

2.正常的conv运算，得到[W， H， Output x 4]大小的output tensor。

3.使用depth_to_space操作，将output tensor的大小变为[W x 2， H x 2， Output]。

显然，kernel padding只用算一次，且可预计算，因此计算效率上比input padding高得多。

## Deconvolution & Image Resize

Deconvolution提供了比普通的Image Resize更丰富的上采样方式。因此，常规的Image Resize操作，实际上都可用Deconvolution来做。这在某些拥有NN硬件加速的设备上是很有用的。

参考：

https://cv-tricks.com/image-segmentation/transpose-convolution-in-tensorflow/

Image Segmentation using deconvolution layer in Tensorflow

https://zhuanlan.zhihu.com/p/32414293

双线性插值的两种实现方法

http://warmspringwinds.github.io/tensorflow/tf-slim/2016/11/22/upsampling-and-image-segmentation-with-tensorflow-and-tf-slim/

Upsampling and Image Segmentation with Tensorflow and TF-Slim

## Dilated convolution

![](/images/article/dilation.gif)

上图是Dilated convolution的操作。又叫做多孔卷积(atrous convolution)。

可以看出，它和Deconvolution的差别在于，前者是kernel上有洞，而后者是Input上有洞。

和池化相比，Dilated convolution实际上也是一种下采样，只不过采样的位置是固定的，因而能够更好的保持空间结构信息。

Dilated convolution在CNN方面的应用主要是Fisher Yu的贡献。

论文：

《Multi-Scale Context Aggregation by Dilated Convolutions》

《Dilated Residual Networks》

代码：

https://github.com/fyu/dilation

https://github.com/fyu/drn

>Fisher Yu，密歇根大学本硕+普林斯顿大学博士。   
>个人主页：   
>http://www.yf.io/

和Deconvolution类似，Dilated convolution也可以采用space_to_batch和batch_to_space操作，将之转换为普通卷积。

参考：

https://zhuanlan.zhihu.com/p/28822428

Paper笔记：Dilated Residual Networks

## 分组卷积

![](/images/article/AlexNet.png)

分组卷积最早在AlexNet中出现，由于当时的硬件资源有限，训练AlexNet时卷积操作不能全部放在同一个GPU处理，因此作者把feature maps分给2个GPU分别进行处理，最后把2个GPU的结果进行融合。

在AlexNet的Group Convolution当中，特征的通道被平均分到不同组里面，最后再通过两个全连接层来融合特征，这样一来，就只能在最后时刻才融合不同组之间的特征，对模型的泛化性是相当不利的。

为了解决这个问题，ShuffleNet在每一次层叠这种Group conv层前，都进行一次channel shuffle，shuffle过的通道被分配到不同组当中。进行完一次group conv之后，再一次channel shuffle，然后分到下一层组卷积当中，以此循环。

![](/images/img2/ShuffleNet.png)

论文：

《ShuffleNet: An Extremely Efficient Convolutional Neural Network for Mobile Devices》

![](/images/img2/ShuffleNet_2.png)

上图是ShuffleNet的Unit结构图，DWConv表示depthwise convolution，GConv表示pointwise group convolution。a是普通的Deep Residual Unit，b的进化用以提高精度，c的进一步进化用以减少计算量。
