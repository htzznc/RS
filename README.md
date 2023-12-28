# RS
推荐系统学习

在这里记录我的推荐系统学习记录


# [笔记](./mynotes/推荐系统.md)
一些学习过程中的笔记。可能不太全。
详见 **mynotes** 目录


# [音乐推荐](./music_rec/README.md)

ItemCF, GBDT+LR 的实践
（这里插一嘴，音乐推荐 spotify 算是鼻祖， 并且也发布了一些可以用作音乐推荐的工具包，有兴趣的可以去了解下spotify的发家之路。

# DIN 论文阅读以及复现

用户行为序列建模的开山之作，经典必读论文。
需要掌握基本结构，以及论文中提出的 mini-batch正则化的思想， GAUC这一指标的计算方法以及提出原因，还有让激活函数适应数据分布的Dice激活函数。


# Recsys 2022 Challenge


## ItemCF

## DeepWalk 构建 embedding

## Commirec-SA   多兴趣召回方法
使用movie-Lens数据集，

## Wide & Deep
使用了criteo的采样子数据集，这里有13个连续特征和26个类别特征。

首先要填充数据的空缺值，这里连续特征用0，类别特征用no进行缺失值补全。

连续特征的值就是一个数字，没有进行处理
26个类别特征分别有不同的值域，有的特征有几十万种可能取值，有的只有3 4种，
这里对这26个特征分别设置embedding层进行embedding

wide侧使用简单的LR，输入特征用的是类别特征

deep侧就是一个3层带Relu的MLP

然后将两侧的预测相加进行损失计算以及梯度回传。

## MMoE

# DeepFM
