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
3. 
