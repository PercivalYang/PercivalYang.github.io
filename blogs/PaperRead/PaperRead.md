# Mutual paper

| Name                                          | Year | Comment | Abstract                                                     |
| --------------------------------------------- | ---- | ------- | ------------------------------------------------------------ |
| [MutualNet](https://arxiv.org/abs/1909.12978) | 2019 | ECCV    | one teacher net and three sub-nets, sub-nets' architecture is same as teacher net, but their width is smaller than teacher's. Using different image's resolution to input different net, e.g. $224^2$ images input teacher network, and $192^2$ images input the first net whose width is     0.8$\times Width_{teacher}$ ... |
|                                               |      |         |                                                              |

# Distillation

| Name                                                         | Year | Abstract                                                     |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| [Subclass Distillation](https://arxiv.org/abs/2002.03936)    | 2020 | 对于多分类问题，学生网络能通过KD的方法从教师网络蒸馏出有用的知识，这些经过Soften的知识不仅包含正确标签和错误标签间的关系，还包含错误标签之间的关系，但是对于二分类问题学生智能蒸馏出正确与错误标签之间的知识。因此本篇文章针对此问题，并让教师网络在Binary Classification 中创造新的Subclass，并引入Auxiliary loss 加速并提高二分类问题蒸馏出来的学生网络的精度<br />Question:<br />1. Subclass 是怎么创建的；<br />2. Auxiliary Loss的作用还没看懂 |
| [Improved Knowledge Distillation via Teacher Assistant](https://ojs.aaai.org/index.php/AAAI/article/view/5963) | 2020 | 在KD中如果教师网络和学生网络相差太大(如ResNet101和ResNet18)，在之间加入一个TA(Teacher Assistant)有助于提高精度。<br />Question:<br />1.如何选择TA？<br />2.应该加几个TA？<br />Answer:<br />1. TA的选择论文作者根据教师网络和学生网络在该数据集上的平均精度来选择(例如直接训练ResNet18在CIFAR-100上的精确度是40%，ResNet101精度是50%，他们的平均值为45%，则选取离45%精度最近的ResNet网络来当TA)，而不是取层数的中间值进行选择；<br />2. 可以按照方案1的选择方法选取多个TA，但这样会提高成本同时获取的精度提升并不是很大.(根据实际情况判别) |



# Others

| Name                                                         | Year | Comment | Abstract                                                     |
| ------------------------------------------------------------ | ---- | ------- | ------------------------------------------------------------ |
| [Explaining Knowledge Distillation by Quantifying the Knowledge]([https://arxiv.org/abs/2003.03622]) | 2020 | CVPR    | 从3个方面分析为什么KD是有效果的：1.KD让DNN学到更多的visual concepts; 2.KD确保DNN在不同图片上能够同步地学到各种有用的visual concepts; 3.比起从0训练, KD能指引学生网络往相对正确的学习方向训练 |
| [Label Refinery](https://arxiv.org/abs/1805.02641)           | 2018 |         | 第一个网络根据Ground truth label(Hard target)进行学习，train好第一个网络后，train第二个网络将第一个网络的输出作为label(soft target)，以此类推训练第三个、第四个 |
| [Self-training with Noisy Student improves ImageNet classifification](https://openaccess.thecvf.com/content_CVPR_2020/html/Xie_Self-Training_With_Noisy_Student_Improves_ImageNet_Classification_CVPR_2020_paper.html) | 2020 | CVPR    | 先用教师网络EffecientNet-B7在有label的数据集上训练，然后再用更大的EffecientNet-L2在之前有label的数据集+没有label的数据集(数量是有label数据集的14倍)上进行训练，其中没有label的数据集会先由之前训练好的EffecientNet-B7生成伪标签在代入ENet-L2种训练，将ENet-L2看作学生网络，对其采用Dropout, Stochastic depth, RandAugment 来增强其泛化能力.训练完第一个学生网络后再将其作为教师网络训练下一个ENet-L2，以此类推<br />和KD不同的是，这里的学生网络可以和教师网络一样大甚至比教师网络大，同时KD的目的是蒸馏出小的学生网络，而这的目的是提高网络的泛化能力(类似上面的Label Refinery) |



# Prunning

| Name                                                         | Year | Abstract                                                     |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| **[Learning both Weights and Connections for Effificient](https://arxiv.org/abs/1506.02626)** | 2015 | 没理解透，此处只对文中一些觉得重要的地方进行记录：<br />1.先学习连接层之间的关系，找出informative 的feature map, 然后不重要的prunning 掉，然后再retrain 获取新weight;<br />2.L2 norm 相比L1 norm 能获得更好的结果；<br />3. Iterative prune 和 retrain帮助非常大<br />4. 比起prunning fc layer，prunning conv layer 更容易影响模型的性能； |
| **AutoSlim: Towards One-Shot Architecture Search for Channel Numbers** | 2019 | 1.在这之前还有两篇前置文献需要阅读，分别是Slimmable network, Universally slimmable networks and improved training techiniques；<br />2.主要的流程图如下：<br />1）先确定一个网络架构（如ResNet50，MobileNet等）；<br />2）训练此网络架构下的slimmable模型（对网络的通道进行瘦身，通常保留低位坐标的channels）；<br />3）训练好的slimmable 模型可以作为原网络瘦身过程中的一个estimator，通过此estimator网络进行不断地迭代评估和瘦身；<br />4）设定一个目标阈值，达到阈值后网络停止瘦身。![image-20220314164535939](https://gitee.com/percivalyang/images/raw/master/images/image-20220314164535939.png) |
| **Learning Effificient Convolutional Networks through Network Slimming** | 2017 | 1.Channel-level 的剪枝；<br />2.引入缩放因子$\gamma$，损失函数计算如下，加号前为正常损失函数计算，加号后为正则项，其中$g(\cdot)$采用L1正则化<br />![image-20220320210412641](https://gitee.com/percivalyang/images/raw/master/images/image-20220320210412641.png)<br />3.在Batch Normalization中对channel的输出的处理如下：<br />![image-20220320210653650](https://gitee.com/percivalyang/images/raw/master/images/image-20220320210653650.png)<br />4.由于BN中有缩放因子参数$\gamma$，可直接用来作为可学习的参数，代入上方损失函数进行训练网络模型（Train with Sparsity) |

​	

# Quantization

| Name | Year | Abstract |
| ---- | ---- | -------- |
|      |      |          |

