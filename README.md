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
        2. 将模糊的图片变的清晰，如csdn木盏先生所述的去雨，去雾，去抖动，去马赛克等
        3. 进行数据增强，如csdn木盏先生所述根据已有数据生成更多新数据供以feed，可以减缓模型过拟合现象
下面解释一下什么叫过拟合：
