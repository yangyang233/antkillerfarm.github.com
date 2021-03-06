---
layout: post
title:  深度学习（二十三）——MemNet, RDN, ShuffleSeg, SVDF, LCNN, AI前沿, LSTM进阶
category: DL 
---

# MemNet

MemNet是南京理工大学的作品。

论文：

《MemNet: A Persistent Memory Network for Image Restoration》

代码：

https://github.com/tyshiwo/MemNet

![](/images/img2/MemNet.png)

![](/images/img2/MemNet_2.png)

![](/images/img2/MemNet_3.png)

没啥好讲的，无非RNN和Resnet在原理上是等价的而已。结构上和DRCN几乎一样，不知道谁抄谁。。。

参考：

https://mp.weixin.qq.com/s/KxQ-GRnEYEdmS2H-DHIHOg

南京理工大学ICCV 2017论文：图像超分辨率模型MemNet

# RDN

Residual Dense Network是美国东北大学的张宇伦的作品。

>Yulun Zhang，西安电子科技大学本科（2013年）+清华硕士（2017年），现为博士一年级。   
>个人主页：   
>http://yulunzhang.com/

论文：

《Residual Dense Network for Image Super-Resolution》

![](/images/img2/RDN.png)

该论文在比较Residual block和Dense block的基础之上，提出了Residual dense block。

![](/images/img2/RDN_2.png)

![](/images/img2/RDN_3.png)

中规中矩的论文吧，熟悉Residual block和Dense block的人应该能秒懂，不多说了。

这类基本结构的SR应用除了MemNet和RDN之外，还有更早的SRResnet和SRDensenet，光听名字估计就知道是怎么回事了，灌水利器啊！

参考：

https://mp.weixin.qq.com/s/_r3MKxMTIR856ezEozFOGA

残差密集网络：利用所有分层特征的图像超分辨率网络

# ShuffleSeg

ShuffleSeg是开罗大学的Mostafa Gamal和Mennatullah Siam的作品（2018.3）。看名字应该是阿拉伯人，而且一男一女。

论文：

《ShuffleSeg: Real-time Semantic Segmentation Network》

代码：

https://github.com/MSiam/TFSegmentation

![](/images/img2/ShuffleSeg.png)

这是一个语义分割的网络，本来不该放在这里。然而既然要灌水，那就灌的更猛一些吧。ShuffleNet也难逃毒手。

参考：

https://mp.weixin.qq.com/s/W2reKR5prcf3_DMp53-2yw

新型实时形义分割网络ShuffleSeg：可用于嵌入式设备

# SVDF

SVDF是UCB和Google Speech Group的作品，主要用于简化Speech模型的计算量。

论文：

《Compressing Deep Neural Networks using a Rank-Constrained Topology》

代码：

https://github.com/tensorflow/tensorflow/blob/master/tensorflow/examples/speech_commands/models.py

音频数据通常是一个[time, frequency]的二维tensor，直接放入FC网络，会导致较大的计算量。（下图左半部分所示）

![](/images/img2/SVDF.png)

SVDF将每个time的frequency作为一组，进行FC之后，再和其他组的结果进一步FC。上图右半部分所示的是time的filters为1的时候的SVDF。当然filters也可以为其他值，和CNN类似，filters越多，提取的特征越多。

从原理来说，SVDF相当于用两层FC来拟合1层FC，即：

$$w_{i,j}^{(m)}\approx \alpha_i^{(m)}\beta_i^{(m)}$$

SVDF将运算量从$$Cd$$变为$$(C+d)k$$，这里的k为filters numbers。

这实际上就是2维tensor的SVD，只不过SVD是线性变换，而这里是非线性变换而已。（参见《机器学习（十五）》中的ALS算法部分）

实际上，SVDF和之前在《深度学习（十六）》中提到的Fast R-CNN的FC加速，原理是基本一致的。

# LCNN

LCNN是华盛顿大学和Allen AI研究所的作品。后者是微软创始人Paul Allen投资兴建的研究机构。

论文：

《LCNN: Lookup-based Convolutional Neural Network》

代码：

https://github.com/hessamb/lcnn

我们知道一个Conv层的weight是一个$$n\times m\times k_w \times k_h$$的tensor，这里的m,n分别是input和output的channel数，$$k_w,k_h$$则是kernel的宽和高。

LCNN将这个巨大的weight tensor拆解成若干小tensor的运算：

1.建立一个包含k个$$m\times k_w \times k_h$$大小的tensor的字典D。

2.一个用于选择字典条目的矩阵I。

3.权值矩阵C。

然后按照下图所示的方法，计算得到W：

![](/images/img2/LCNN.png)

用数学公式表示，则为：

$$W_{[:,r,c]}=\sum_{t=1}^sC_{[t,r,c]}\cdot D_{[I_{[t,r,c]},:]},\forall r,c$$

![](/images/img2/LCNN_2.png)

上图是LCNN的前向运算示意图，其中:

$$S_{[i,:,:]}=X*D_{[i,:]}$$

这个过程实际上等效于$$S*P$$，而参数P就是我们需要训练的模型参数。

可以看出LCNN和SVDF都是采用稀疏表示的方法来减少运算量，只是实现方式和用途略有不同而已。

参考：

http://blog.csdn.net/feynman233/article/details/69785592

LCNN论文阅读笔记

# AI前沿

人工智能前沿7大热点：

1.强化学习

2.元学习

3.模仿学习

4.机器人

5.概念与抽象

6.感知与意识

7.因果推理

参考：

https://mp.weixin.qq.com/s/QtO-4ARpAQf0kXfALqMKSQ

DeepMind-深度学习: AI革命及其前沿进展

https://mp.weixin.qq.com/s/sji2HVli-Y7am37YjTbq3w

谷歌Jeff Dean 64页 PPT 讲述《用深度学习解决挑战性问题》

https://mp.weixin.qq.com/s/AQrgvjFPXUpqfqQQgOFN9A

36页最新深度学习综述论文：算法、技术、应用，181篇参考文献

https://mp.weixin.qq.com/s/cGKsZYxrVP7hVnv7Jli9Zg

MIT课程全面解读2019深度学习最前沿

# LSTM进阶

## 《Long short-term memory》

这是最早提出LSTM这个概念的论文。这篇论文偏重数学推导，实话说不太适合入门之用。但既然是起点，还是有列出来的必要。

## 《LSTM Neural Networks for Language Modeling》

这也是一篇重要的论文。

## 《Sequence to Sequence - Video to Text》

https://vsubhashini.github.io/s2vt.html

![](/images/article/S2VTarchitecture.png)

参考：

https://mp.weixin.qq.com/s/HqffHVMKJkA6H1E9ItQU4A

《sequence to sequence: video to text》视频描述的全文翻译

## 《Long-term Recurrent Convolutional Networks for Visual Recognition and Description》

Long-term Recurrent Convolutional Networks是LSTM的一种应用方式，它结合了LSTM、CNN、CRF等不同网络组件。

![](/images/article/LSTM_X.png)

上图展示了LSTM在动作识别、图片和视频描述等任务中的网络结构。

![](/images/article/LSTM_X_2.png)

上图展示了图片描述任务中几种不同的网络连接方式：

1.单层LRCN。

2.双层LRCN。CNN连接在第一个LSTM层。传统的LSTM只有一个输入，这里的CNN是第二个输入，也就是所谓的静态输入。可参看caffe的LSTM实现。

2.双层LRCN。CNN连接在第二个LSTM层。

![](/images/article/LSTM_X_3.png)

![](/images/article/LSTM_X_4.png)

![](/images/article/LSTM_X_5.png)

这是视频描述任务中LSTM和CRF结合的示例。

## 《Training RNNs as Fast as CNNs》

这篇论文提出了如下图所示的Simple Recurrent Unit（SRU）的新结构：

![](/images/article/SRU.jpg)

由于普通LSTM计算步骤中，很多当前时刻的计算都依赖$$h_{t-1}$$的值，导致整个网络的计算无法并行化。SRU针对这一点去掉了当前时刻计算对于$$h_{t-1}$$的依赖，而仅保留$$C_{t-1}$$（这个计算较为廉价）以记忆信息，大大改善了整个RNN网络计算的并行性。

但是SRU的精度没有LSTM高，需要通过增加layer和filter的数量来达到相同的精度，当然即使这样，计算时间仍然小于LSTM。

参考：

https://mp.weixin.qq.com/s/PsIa3XDFqZlY2tKcvqvddw

Training RNNs as Fast as CNNs

## 《Neural Machine Translation in Linear Time》

该论文是Deepmind的作品，它提出的ByteNet，计算复杂度为线性，也是LSTM的优化方案之一。

## 《Long Short-Term Memory Based Recurrent Neural Network Architectures for Large Vocabulary Speech Recognition》

$$
i_t=\delta(W_{ix}x_t+W_{im}m_{t-1}+W_{ic}c_{t-1}+b_i)\\
f_t=\delta(W_{fx}x_t+W_{fm}m_{t-1}+W_{fc}c_{t-1}+b_i)\\
c_t=f_t\odot c_{t-1}+i_t\odot g(W_{cx}x_t+W_{cm}m_{t-1}+b_c)\\
o_t=\delta(W_{ox}x_t+W_{om}m_{t-1}+W_{oc}c_{t}+b_o)\\
m_t=o_t\odot h(c_t)\\
y_t=W_{ym}m_t+b_y
$$

上式是LSTM的公式（其中的最后一步在多数模型中，往往直接用$$y_t=m_t$$代替。），从中可以看出类似$$W_{ix}x_t+W_{im}m_{t-1}+W_{ic}c_{t-1}+b_i$$的FC运算占据了LSTM的绝大部分运算量。其中W的参数量为：

$$W=\color{blue}{n_c\times n_c\times 4}+n_i\times n_c\times 4+\color{red}{n_c\times n_o}+n_c\times 3$$

为了精简相关运算，Google的Hasim Sak于2014年提出了LSTMP。

>Hasim Sak，土耳其伊斯坦布尔海峡大学博士，Google研究员。

LSTMP的结构图如下：

![](/images/img2/LSTMP.png)

改写成数学公式就是：

$$
i_t=\delta(W_{ix}x_t+W_{im}r_{t-1}+W_{ic}c_{t-1}+b_i)\\
f_t=\delta(W_{fx}x_t+W_{fm}r_{t-1}+W_{fc}c_{t-1}+b_i)\\
c_t=f_t\odot c_{t-1}+i_t\odot g(W_{cx}x_t+W_{cm}r_{t-1}+b_c)\\
o_t=\delta(W_{ox}x_t+W_{om}r_{t-1}+W_{oc}c_{t}+b_o)\\
m_t=o_t\odot h(c_t)\\
r_t = W_{rm}m_t\\
p_t = W_{pm}m_t\\
y_t = W_{yr}r_t + W_{yp}p_t + b_y
$$

LSTMP的主要思想是对$$m_t$$做一个映射，只有部分数据$$r_t$$参与recurrent运算，其余部分$$p_t$$直接输出即可（这一步是可选项，所以用虚框表示）。

这样W的参数量为：

$$W=\color{blue}{n_c\times n_r\times 4}+n_i\times n_c\times 4+\color{red}{n_r\times n_o+n_c\times n_r}+n_c\times 3$$

参数量公式用蓝色和红色标出修改前后对应的部分，可以看出计算量有了明显下降。

参考：

http://blog.csdn.net/xmdxcsj/article/details/53326109

模型压缩lstmp

