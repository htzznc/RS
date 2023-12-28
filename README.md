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
### deepwalk构建
此目录使用session——item的信息 以交互时间从远到近排序，构建了行为序列。

以构建出的行为序列  如
session[ 12345] 的行为序列为  'item_9655'，'item_9233'，'item_155'

作为构建deepwalk图的依据

### deepwalk步骤
构建好deepwalk的图之后进行deepwalk步骤

随机选取一个item A， 然后在 item A指向的item中随机选取一个 item B  这样依次走
直到序列长度到达预期  这里选择了序列长度为16

走了100w个这样的路径 

将这100w个item路径输入 genius库的word2vec模型中 训练
### 结果
得到了item的embedding表示  ，并且可以通过item embedding表示计算item之间的相似度  进行I2I推荐
## Commirec-SA   多兴趣召回方法
使用movie-Lens数据集，
对兴趣向量和目标item做attention，选择相似度最大的那个兴趣向量做loss计算
将用户的交互行为按照时间排序，构建   用户:物品池  随机选择物品池中的一个物品，将其前N（本次实验中是20）个交互作为历史行为序列， 不足N 则用 0 padding 并构建mask

将用户行为序列输入 多兴趣提取模块  对多兴趣提取模块设置 K（兴趣向量的个数）
$H^{d*n}$ n为序列长度 d为embedding_dim
attention
$$ A = softmax(W_2^T tanh(W_1H))^T $$
最终的兴趣向量
$$V_u = HA $$


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
