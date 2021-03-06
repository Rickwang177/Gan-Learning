# Gan-Learning
Record the gan learning
**在此记录关于生成对抗神经网络Gan的有关学习记录**

**生成对抗神经网络：Generative adversarial network**

**首先我将给出关于生成对抗神经网络的一个英文解释说明：**
Generative:可译为生产的、有生产力的
adversarial：对抗的
network：网络

**Gan提出的初衷：**

Gan提出的初衷就是生成一个不属于真实世界中的东西（捏造、伪造、仿造）
Gan可以用来做：        
        1. 充分发挥Gan的创造性，进行没有限制的创作
        2. 将模糊的图片变的清晰，如去雨，去雾，去抖动，去马赛克等（此处引用csdn 木盏先生）
        3. 进行数据增强，如csdn木盏先生所述根据已有数据生成更多新数据供以feed，可以减缓模型过拟合现象
本处的名词解释：
1. 下面解释一下什么叫过拟合：
   1.1 基本概念：
       所建的机器学习模型或者是深度学习模型在训练样本中表现得过于优越，导致在验证数据集以及测试数据集中表现不佳
       （仅仅是在训练样本上面表现良好，实际应用到测试集和验证数据集上面表现不佳）
   
   1.2 从性能的角度去看待：
       在性能的角度上讲是协方差过大（variance is large），同样在测试集上的损失函数（cost function）会表现得很大（此处引用csdn Wuhua Jr.先生的话）
   
   1.3 造成过拟合的原因：
       造成过拟合的原因可以归结为：参数过多，那么我们需要做的事情就是减少参数（此处引用csdn Wuhua Jr.先生）
   
   1.4 怎么进行减少参数（此处引用csdn Wuhua Jr.先生）：
   
      1.4.1 方法一：
      
         回想下我们的模型，假如我们采用梯度下降算法将模型中的损失函数不断减少，那么最终我们会在一定范围内求出最优解，最后损失函数不断趋近0。那么我们可以在所定义的损失函数后       面加入一项永不为0的部分，那么最后经过不断优化损失函数还是会存在。其实这就是所谓的“正则化”。下面这张图片就是加入了正则化（regulation）之后的损失函数。这里m是样本数         目，landa（后面我用“t”表示，实在是打不出）表示的是正则化系数。
      ![image](https://user-images.githubusercontent.com/87885188/178662220-bb586bb6-e393-4596-8622-05e5b265830d.png)
         注意：当t（landa）过大时，则会导致后面部分权重比加大，那么最终损失函数过大，从而导致欠拟合，当t（landa）过小时，甚至为0，导致过拟合。
         
      1.4.2 方法二：
      
         对于神经网络，参数膨胀原因可能是因为随着网路深度的增加，同时参数也不断增加，并且增加速度、规模都很大。那么可以采取减少神经网络规模（深度）的方法。也可以用一种           dropout的方法。dropout的思想是当一组参数经过某一层神经元的时候，去掉这一层上的一部分神经元，让参数只经过一部分神经元进行计算。注意这里的去掉并不是真正意义上的去除，       只是让参数不经过一部分神经元计算而已。
      ![image](https://user-images.githubusercontent.com/87885188/178662563-c6fe529e-aff6-4c81-a37c-70692508e50b.png)
      
      1.4.3 方法三：
      
         另外增大训练样本规模同样也可以防止过拟合。

2. 下面解释一下什么叫协方差：
   2.1 首先我们给出均值、方差、标准差的公式
      ![image](https://user-images.githubusercontent.com/87885188/178680904-7bb6c6d1-4f26-468a-9936-ad2795a2a24a.png)
      现在我们对概念进行解释：
         1. 均值描述的是样本集合的中间点，它告诉我们的信息是很有限的
         2. 标准差描述的则是样本集合的各个样本点到均值的距离之平均，标准差描述的就是这种“散布度”， 之所以除以n-1而不是除以n，是因为这样能使我们以较小的样本集更好的逼近总体             的标准差，即统计上所谓的“无偏估计”
         3. 方差则仅仅是标准差的平方
    2.2 为什么需要协方差？
       现实生活我们常常遇到含有多维数据的数据集，最简单的大家上学时免不了要统计多个学科的考试成绩。面对这样的数据集，我们当然可以按照每一维独立的计算其方差，但是通常我们还想     了解更多，比如，一个男孩子的帅气程度跟他受女孩子欢迎程度是否存在一些联系啊，协方差就是这样一种用来度量两个随机变量关系的统计量
    2.3 协方差的公式引出：
       参考方差的公式：
       ![image](https://user-images.githubusercontent.com/87885188/178681293-9447a7d1-2204-4198-8406-826abf3e3ae0.png)
       从而提出协方差的公式：
       ![image](https://user-images.githubusercontent.com/87885188/178681431-7785efbf-5fec-4cc9-820b-107a79e9dcd2.png)
    2.4 协方差的结果有什么意义呢？
       如果结果为正值，则说明两者是正相关的(从协方差可以引出“相关系数”的定义)，也就是说一个人越帅气就越受女孩子欢迎，结果为负值就说明负相关的，越帅气女孩子越讨厌，如果为0，        也是就是统计上说的“相互独立”。
    2.5 协方差的性质
    ![image](https://user-images.githubusercontent.com/87885188/178681583-b108f6ab-be86-4fa8-8e98-efee38cdc8c4.png)
    2.6 协方差矩阵
       协方差也只能处理二维问题，那维数多了自然就需要计算多个协方差，比如n维的数据集就需要计算
       
       \frac{n!}{(n-2)!\ *\ 2} 
       
       个协方差，那自然而然的我们会想到使用矩阵来组织这些数据，由此给出协方差矩阵的定义： 
       
       假设数据集有三个维度，则协方差矩阵为
       ![image](https://user-images.githubusercontent.com/87885188/178681703-cb564f7b-0f46-45fd-b76c-cae36edfbbd9.png)
       
       协方差矩阵是一个对称的矩阵，而且对角线是各个维度上的方差
       2.7 Matlab协方差实战
3. 下面解释一下什么叫协方差：
