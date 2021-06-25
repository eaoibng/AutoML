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

***

早期的网络架构搜索面临着以下几个问题：

1. 全局搜索策略：搜索网络结构的所有部分，在巨大的搜索空间中找到最优，无异于大海捞针；
2. 离散的搜索空间：通过离散地修改来改变网络结构，意味着不能使用梯度策略来调整网络结构；
3. 从头搜索：从零构建模型，这种方法不能很好的利用原来已经设计好的优秀的网络结构，浪费时间；
4. 完全训练：将每个候选网络从头训练直到收敛。后续的网络和先前的网络在结构上存在相似之处，从头训练不能充分利用这一关系；

***

后续的一些优化策略，比如模块化搜索策略，连续搜索空间，网络架构回收，不完全训练等。

***Modular Search Strategy***

简化搜索空间，把网络切分成基本的单元(cell/block)，有效的减少了搜索空间。

NASNet最早探索了这种基于cell的搜索方法，提出搜索两种类型的单元：normal cell、reduction cell。

ENAS也证明了搜索cell结构的有效性。

***Continuous Search Space***

DARTS使用了Softmax将原来离散的搜索空间连续化，在保证搜索到的网络性能的同时，大大降低了计算开销。

在连续搜索空间中使用梯度优化方法寻找合适的网络结构是一个重要趋势。

***Network Architecture Recycle***

以现有的人工设计的优秀网络结构为出发点，利用NAS方法对它们修改、演化，从而得到新的具有潜力的高性能模型，通常将这个过程称作网络迁移，这种方法使得NAS大量使用前人设计好的高性能网络成为可能。代表工作：Net2Net, Efficient Architecture Search(EAS), Path-level EAS, NASH-Net, Fast Neural Network Adaptation(FNA)。

***Incomplete Training***

训练不必从头——权值共享

在迁移学习或多任务学习中，通过训练某一为特定任务设计的特定模型而得到的参数，是可以用于其他任务/模型的。ENAS是第一个提出参数共享的NAS论文，指出候选网络架构可以看作一个超网络结构中sampled的有向无环子图，强制子网络之间共享参数，这样子网络就不必从头训练。

不必训练至收敛

在NAS中，对于有潜力的候选网络结构，可以进一步进行充分训练，对于没有潜力的网络架构，可以提早停止。模型训练过程中，往往可以根据学习曲线来判断学习情况。

***

一些搜索方法的缩写：

强化学习(Reinforcement learning，RL)

进化算法(Evolutionary algorithm，EA)

梯度优化方法(Gradient optimization，GO)

随机搜索(Random Search，RS)

SMBO模型(Sequential model-based optimization，SMBO，贝叶斯优化的最简形式)

***

