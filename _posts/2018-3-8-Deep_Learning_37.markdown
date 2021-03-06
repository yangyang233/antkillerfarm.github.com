---
layout: post
title:  深度学习（三十七）——人脸检测/识别（2）, 多模态学习
category: DL 
---

# 人脸检测/识别

## 人脸识别

人脸检测是从一张图片中，识别出人脸，这和通常的目标检测没有太大的差别。**而人脸识别，则是精确到具体的人。**

人脸识别通常的做法是：

1.使用人脸检测，得到人脸区域的图像。

2.提取人脸特征。一般采用CNN+FC+loss的结构。其中，CNN+FC用于提取特征，而loss仅用于训练阶段。在推理阶段，我们使用CNN+FC得到人脸的特征向量即可。

3.特征的对比。比较两个特征向量的相似度（可以使用LMS或者cos相似度）。超过阈值，即认为是同一张脸。

## OHEM

论文：

《Training Region-based Object Detectors with Online Hard Example Mining》

代码：

https://github.com/abhi2610/ohem

参考：

https://blog.csdn.net/zimenglan_sysu/article/details/51318058

论文笔记

https://blog.csdn.net/Wayne2019/article/details/78945099

OHEM，Batch Hard（识别乱入），Focal Loss

https://blog.csdn.net/Z5337209/article/details/72838049

Faster R-CNN 深入理解 && 改进方法汇总

https://zhuanlan.zhihu.com/p/28202204

困难样本挖掘

https://zhuanlan.zhihu.com/p/34179420

目标检测入门（二）：模型的评测与训练技巧

## FaceNet

论文：

《FaceNet: A Unified Embedding for Face Recognition and Clustering》

https://blog.csdn.net/stdcoutzyx/article/details/46687471

FaceNet--Google的人脸识别

## OpenFace

OpenFace是一款开源的人脸识别软件。它的原理基于CVPR 2015年的论文：FaceNet。由于采用了深度学习技术，OpenFace对人脸识别的准确率，大大超过了OpenCV。

OpenFace是用Python和Torch编写的。

官网：

https://cmusatyalab.github.io/openface/

参考：

http://www.cnblogs.com/pandaroll/p/6590339.html

开源人脸识别openface

https://mp.weixin.qq.com/s/RSCrkeIToeNKrFvMITxzDg

通过OpenFace来理解人脸识别

## SeetaFace

SeetaFace人脸识别引擎由中科院计算所山世光研究员带领的人脸识别研究组研发。代码基于C++实现，且不依赖于任何第三方的库函数，开源协议为BSD-2，可供学术界和工业界免费使用。

代码：

https://github.com/seetaface

论文：

《Coarse-to-Fine Auto-Encoder Networks (CFAN) for Real-Time Face Alignment》

参考：

https://zhuanlan.zhihu.com/p/22451474

SeetaFace开源人脸识别引擎介绍

http://www.cnblogs.com/nenya33/p/6801045.html

CFAN

## Siamese network

https://blog.csdn.net/shenziheng1/article/details/81213668

Siamese Network（原理篇）

https://www.jianshu.com/p/92d7f6eaacf5

Siamese network孪生神经网络--一个简单神奇的结构

https://blog.csdn.net/sxf1061926959/article/details/54836696

Siamese Network理解

https://vra.github.io/2016/12/13/siamese-caffe/

Caffe中的Siamese网络

https://mp.weixin.qq.com/s/rPC542OcO8B4bjxn7JRFrw

深度学习网络只能有一个输入吗

## S3FD

https://mp.weixin.qq.com/s/MyA8_yt4YCkFl67AyhpZow

尺度不变人脸检测器（S3FD-Single Shot Scale-invariant Face Detector）

https://github.com/sfzhang15/SFD

S3FD: Single Shot Scale-invariant Face Detector

## 人脸年龄识别

https://zhuanlan.zhihu.com/p/53229759

年龄估计技术综述

https://www.openu.ac.il/home/hassner/projects/cnn_agegender/

Age and Gender Classification using Convolutional Neural Networks

https://mp.weixin.qq.com/s/0hVPateb108B1KpVpYXK0A

人工智能：长相越“娘”颜值越高

https://mp.weixin.qq.com/s/YlrWHDPIPzN4dQO2vo4DjA

人脸颜值研究综述

https://www.oukohou.wang/2019/01/30/face-aging_using_GAN/

论文阅读-人脸老化：Generative Adversarial Style Transfer Networks for Face Aging

https://mp.weixin.qq.com/s/s2SFQgUOZLV-f6auqymVOg

基于Caffe的年龄&性别识别

## 活体检测

https://mp.weixin.qq.com/s/zOnmKSnQctnyx7pKXX-tpQ

活体检测新文解读：利用多帧人脸来预测更精确的深度

https://mp.weixin.qq.com/s?__biz=MzU4MjQ3MDkwNA==&mid=2247486721&idx=1&sn=f0e5b2b0165e391c0d5adc4ce253f2f6

人脸识别中的活体检测算法综述

https://mp.weixin.qq.com/s/A1pbiU5PA9Owe69lGX9afw

活体识别告诉你为什么照片无法破解人脸系统

https://mp.weixin.qq.com/s/sPnoZyCkAhcCs_GtA79DrA

单目可见光静默活体检测Binary or Auxiliary Supervision论文解读

https://mp.weixin.qq.com/s/Vi2ypwO3uCD2lQZOwDFqTA

基于rPPG的人脸活体检测综述

## DeepFace

《DeepFace: Closing the Gap to Human-Level Performance in Face Verification》

DeepFace先进行了两次全卷积＋一次池化，提取了低层次的边缘／纹理等特征。

后接了3个Local-Conv层，这里是用Local-Conv的原因是，人脸在不同的区域存在不同的特征（眼睛／鼻子／嘴的分布位置相对固定），当不存在全局的局部特征分布时，Local-Conv更适合特征的提取。

## 人脸关键点

https://zhuanlan.zhihu.com/p/42968117

人脸关键点检测综述

https://mp.weixin.qq.com/s/CvdeV5xgUF0kStJQdRst0w

从传统方法到深度学习，人脸关键点检测方法综述

https://mp.weixin.qq.com/s/ZrnAqDJCLtMy_qTQ2RZT0A

级联MobileNet-V2实现人脸关键点检测

https://mp.weixin.qq.com/s/ymeJPUPRAGb1FltskqBs-A

人脸关键点检测汇总

## 参考

https://github.com/ChanChiChoi/awesome-Face_Recognition

不止面部识别，一切关于人脸AI的资源都能在这里下载

https://mp.weixin.qq.com/s/eZ78biXN-mVw3s9Ky_LBZg

如何走近深度学习人脸识别？你需要这篇超长综述

https://mp.weixin.qq.com/s/tum24mzS2cUiKW87a1weFA

人脸识别全面总结：从传统方法到深度学习

https://mp.weixin.qq.com/s/bFnuGu4xLJiRfANi0Rkduw

人脸识别的前世今生：从人工特征的百花齐放到深度学习的一统江湖

https://zhuanlan.zhihu.com/p/32702868

人脸检测背景介绍和发展现状

http://mp.weixin.qq.com/s/KQxGQdLa3XzKVIFYqlrV7g

人脸检测与识别的趋势和分析

https://zhuanlan.zhihu.com/p/25335957

人脸检测与深度学习

https://mp.weixin.qq.com/s/a4aPycxfIe_qNIP_vrIZ5w

人脸检测算法综述

http://www.leiphone.com/news/201608/MPXlWtGaJLPYL7NB.html

人脸检测发展：从VJ到深度学习

https://zhuanlan.zhihu.com/p/22591740

从事人脸识别研究必读的N篇文章

https://mp.weixin.qq.com/s/HteNoL3hkjNgUTbGguMflQ

人脸识别技术全面总结：从传统方法到深度学习

https://zhuanlan.zhihu.com/p/56619497

人脸检测江湖的那些事儿——从旷视说起

https://mp.weixin.qq.com/s/7cZTbTBttEvN6NvOarSFgw

如何构建自定义人脸识别数据集

https://mp.weixin.qq.com/s/Z06oUe7oExgkKZ8g2_PnPw

科普人脸表情识别技术

https://mp.weixin.qq.com/s/tS_9gS2ADoEdSKCLB-cxpA

刘小明教授为你讲解人脸识别

https://mp.weixin.qq.com/s/CLgyaAslE4hYHi62UhzeGw

韩琥：深度学习让机器给人脸“贴标签”

https://mp.weixin.qq.com/s/pUcVO8Fj-n9-pMwAzBvWuQ

山世光：人脸识别领域的“激荡20年”

https://mp.weixin.qq.com/s/Gqlo4wU0wtIcJDvQs2kTAw

为了让你分清人脸识别与人脸检测，苹果要亲自给你科普

https://mp.weixin.qq.com/s/ZJmgC8xTruaRLfCocodjqA

人脸检测与识别总结

https://mp.weixin.qq.com/s/lGIkLcglQGvDzdBQmZW0Qw

判别特征学习方法用于人脸识别

https://mp.weixin.qq.com/s/t-vFSkQ7SYlTGGxEEY1mSg

近期人脸对齐的实证性研究

https://mp.weixin.qq.com/s/zhIyZ9MEFXAuIVUxAGkW-w

人脸对齐之GBDT(ERT)算法解读

https://mp.weixin.qq.com/s/1g9PXc_3nhKMf1_-E_cVAA

图像识别的原理、过程、应用前景，精华篇！

https://mp.weixin.qq.com/s/i4HdS-lCrsv9YR39Hja8ow

深度人脸表情识别技术综述，没有比这更全的了

https://mp.weixin.qq.com/s/JY9WXneps-_tYmYhJAFlTg

人脸识别/人证比对《DocFace+: ID Document to Selfie Matching》论文解读

https://mp.weixin.qq.com/s/d3aaN4vGAtMfLqOpU9oC6w

香港中文大学助理教授吕健勤：面向人脸分析的深度学习方法

https://mp.weixin.qq.com/s/Ht8kFTgIWASusfSUQqoaJA

人脸表情识别研究

https://mp.weixin.qq.com/s/qUFjfsDtTQfAEjBCuoWHew

人脸脸型分类研究现状

https://mp.weixin.qq.com/s/wcKUURsYiEYVzn7qTMVPag

格灵深瞳：人脸识别最新进展以及工业级大规模人脸识别实践探讨

https://mp.weixin.qq.com/s/Cy5gxHl_Z4v7BX0k8SDNSQ

AI人像美妆算法初识

https://mp.weixin.qq.com/s/5vx1FGgSOhF71FwHeUwaAQ

清华&商汤开源CVPR2018超高精度人脸对齐算法LAB

https://mp.weixin.qq.com/s/PW_fjdC0hzzwmeY3gUXPkw

如何降低遮挡对人脸识别的影响

https://mp.weixin.qq.com/s/UFOB2V12gQQ3mV-Kh9RTUw

高精度人脸表情识别

https://zhuanlan.zhihu.com/p/35968767

格灵深瞳首席科学家张徳兵：如何进行上亿类的人脸识别？

https://mp.weixin.qq.com/s/b-v_hDHJjUxMithBDr3TcQ

实时旋转鲁棒人脸检测算法

https://blog.csdn.net/xiamentingtao/article/details/50908190

Facial Landmark Detection(人脸特征点检测)

https://mp.weixin.qq.com/s/ZZmLbFzi843g0k3gTncQmA

拿下人脸识别“世界杯”冠军！松下-NUS和美国东北大学实战分享

https://mp.weixin.qq.com/s/DYCXef_09yFFNR0uHL2Q0Q

基于Python的开源人脸识别库：离线识别率高达99.38%

https://mp.weixin.qq.com/s/eOxd5XbeyVcRYyAAmPr20Q

利用空间融合卷积神经网络通过面部关键点进行伪装人脸识别

https://mp.weixin.qq.com/s/vAjWHpn5HP_lwSv49g71SA

新型半参数变分自动编码器DeepCoder：可分层级编码人脸动作

https://mp.weixin.qq.com/s/IS5iAPZeUrvvyWs29O8Ukg

通过提取神经元知识实现人脸模型压缩

https://mp.weixin.qq.com/s/DEJ0z2CahZIrhTE3VXNVvg

基于注意力机制学习的人脸幻构

# 多模态学习

https://mp.weixin.qq.com/s/ruRkqBEdyj2Dx0WTO5Jhcw

多模态学习研究进展综述

https://mp.weixin.qq.com/s/vpBPkjuCebSWh5qPLYHCkw

上海交大提出多模态框架“EmotionMeter”，更精准地识别人类情绪

https://mp.weixin.qq.com/s/BBg04rDtiqU-XrWortufNA

康奈尔&英伟达提出多模态无监督图像转换新方法

http://mp.weixin.qq.com/s/khOINUyrNV3TFfgNRheH0A

卷积神经网络压缩、多模态的语义分析研究

https://mp.weixin.qq.com/s/ywU4L659iRcmIgmV6RtbXA

DeepMind新研究连接听与看，实现“听声辨位”的多模态学习

https://mp.weixin.qq.com/s/1qhcyTXttgKWlw-Oy556Tw

TPAMI2019最新《多模态机器学习综述》

https://mp.weixin.qq.com/s/BczgUuh2FIvP5MG9xh87wQ

多模态多任务学习新论文
