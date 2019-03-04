[TOC]

单词：

> numpy：数组	tensor：张量  discriminative 有区别的，区别对待的
>
> auxiliary 辅助的



# 如何训练一个神经网络





# 梯度爆炸和梯度消失





# 小记录

- 激励函数用于把线性函数变成非线性函数，原理是使用非线性函数与线性函数互相作用（乘，除，映射）

- 激励函数必须是可以微分的, 因为在 backpropagation 误差反向传递的时候, 只有这些可微分的激励函数才能把误差传递回去.

- P ∈ SE(3)  ：SE(3)	是一个三维空间

- [结合SLAM十四讲的示例程序理解SE3, se(3), so(3),R, t等](https://blog.csdn.net/qq_28448117/article/details/79644920)

# 实现步骤

1. 计算所有input images 的语义分割
2. 将图片转换成voxel 地图，分别为：$M_D$和$M_Q$ 
   - 每个voxel的标签有L+2种可能，L为初始数据的标签，另两种为free和unobserved（即空闲和未收集到的某些点）
3. 训练一个语义分类器：如根据季节分类（做什么？：减少因像素导致的光照和地理改变对实验的影响
4. 实验的一个challenge是可靠找到query和database maps的matches



## Generative Descriptor Learning 

- 因为$M_D$ 和$M_Q$的规模是不一样的，所以根据二者subVolumes  $v_D,v_Q$ 来对比发现对应关系

- 该模型需要能够识别出在不同视角，光照时的同一物体

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190304221215902.png)

- 本例使用embedding $f(v)$ 来解决semantic scene understanding，因为另一种方法消耗太大

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190304221539917.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM2MzAzODYy,size_16,color_FFFFFF,t_70)

- $f(v)$函数的作用： $f(v) ∈R _N $ 用于将 subvolume降维：encodes the scene semantics and geometry

- 使用辅助函数$h(v)​$来hallucinate(产生？)缺失部分的地理信息和语义信息

- 使用 3D variational encoder-decoder $h(v)=g(f(v))$, f用于encode 不完整的subvolume，g用于hallucinate(产生) 完整的subvolume，f和g均为神经网络  

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190304223139166.png)

- 

# end

 