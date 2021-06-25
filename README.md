## AutoML笔记

#### 6月25日

阅读论文***A Comprehensive Survey of Neural Architecture Search: Challenges and Solutions***

NAS入门调研论文

***EA、RL***分表表示 遗传算法 以及 强化学习

NAS的总体框架如下图：定义搜索空间(一组可供搜索的神经网络，即决定着NAS可以搜索到哪些网络)，根据搜索策略得到大量候选网络，然后对其训练和排序，作为反馈信息调整搜索策略，之后进一步得到新的候选网络。当满足终止条件时，选出最优网络结构，在测试集上进行评估。

***搜索空间、搜索策略、性能评估策略***是NAS算法的核心要素。

*搜索空间*决定NAS可以搜索到什么样的网络结构；

*搜索策略*告诉机器怎样去搜索；

*性能评估策略*告诉机器如何判断搜索得到的网络的好坏；

<img src="https://github.com/eaoibng/AutoML/raw/main/img/062501.png" alt="NAS" style="zoom:50%;" />



