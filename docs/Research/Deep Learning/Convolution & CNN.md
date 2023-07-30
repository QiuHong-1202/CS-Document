# Convolution & CNN

## 卷积层

- 卷积层将输入和核矩阵进行交叉相关，加上偏移后得到输出
- 核矩阵和偏移是可学习的参数
- 核矩阵的大小是超参数（控制局部性 $\to$ 看的范围）
- 可以看成特殊的全连接层

## 填充和步幅

- 填充和步幅是卷积层的超参数
- 填充在输入周围添加额外的行 / 列, 来控制输出形状的减少量
- 步幅是每次滑动核窗口时的行/列的步长, 可以成倍的减少输出形状

### 填充

- 在输入的周围加入额外的行和列

![image-20230625111324260](./assets/image-20230625111324260.png)

- 填充 $p_h$ 行和 $p_w$ 列, 输出形状为 (p = padding)


$$
\left(n_h-k_h+p_h+1\right) \times\left(n_w-k_w+p_w+1\right)
$$


- 通常取 $p_h=k_h-1, \quad p_w=k_w-1$ (这样输出和输入的 shape 一致)
    - 当 $k_h$ 为奇数：在上下两侧填充 $p_h / 2$
    - 当 $k_h$ 为偶数：在上侧填充 $\left\lceil p_h / 2\right\rceil$, 在 下侧填充 $\left\lfloor p_h / 2\right\rfloor$

### 步幅

- 填充减小的输出大小与层数线性相关
    - 给定输入大小 $224 \times 224$，在使用 $5 \times 5$ 卷积核的情况下，需要 $55$ 层才能将输出降低到 $4 \times 4$
    - 需要大量计算才能得到较小输出

- 步幅是指行/列的滑动步长
    - 例：高度 3，宽度 2 的步幅

![image-20230625120823157](./assets/image-20230625120823157.png)

- 给定高度 $s_h$ 和宽度 $s_w$ 的步幅, 输出形状是


$$
\left\lfloor\left(n_h-k_h+p_h+s_h\right) / s_h\right\rfloor \times\left\lfloor\left(n_w-k_w+p_w+s_w\right) / s_w\right\rfloor
$$


- 如果 $p_h=k_h-1, \quad p_w=k_w-1$


$$
\left\lfloor\left(n_h+s_h-1\right) / s_h\right\rfloor \times\left\lfloor\left(n_w+s_w-1\right) / s_w\right\rfloor
$$


- 如果输入高度和宽度可以被步幅整除


$$
\left(n_h / s_h\right) \times\left(n_w / s_w\right)
$$


## 通道数

- 彩色图像有 RGB 三个通道，因此转换为灰度会丢失信息，所以我们需要多通道的输入
- 每个输出通道可以识别特定模式
- 输入通道核识别并组合输入中的模式

### 多个输入通道

- 每个通道都有一个卷积核，计算结果是所有通道卷积结果的和

![../_images/conv-multi-in.svg](https://zh.d2l.ai/_images/conv-multi-in.svg)


$$
\begin{aligned}
& (1 \times 1+2 \times 2+4 \times 3+5 \times 4) \\
& +(0 \times 0+1 \times 1+3 \times 2+4 \times 3)=56
\end{aligned}
$$


- 输入 $\mathbf{X}: c_i \times n_h \times n_w$
- 核 $\mathbf{W}: c_i \times k_h \times k_w^{\circ}$
- 输出 $\mathbf{Y}: m_h \times m_w$


$$
\mathbf{Y}=\sum_{i=0}^{c_i} \mathbf{X}_{i,:,:}\star \mathbf{W}_{i,:,:}
$$


### 多个输出通道

- 无论有多少输入通道，到目前为止我们只用到单输出通
- 我们可以有多个三维卷积核, 每个核生成一个输出通道
- 输入 $\mathbf{X}: c_i \times n_h \times n_w$
- 核 $\mathbf{W}: c_o \times c_i \times k_h \times k_w$
- 输出 $\mathbf{Y}: c_o \times m_h \dot{\times} m_w$


$$
\mathbf{Y}_{i,:,:}=\mathbf{X} \star \mathbf{W}_{i,:,:,:} \quad \text { for } i=1, \ldots, c_o
$$

### 1x1 卷积层

$k_h=k_w=1$ 是一个受欢迎的选择。它不识别空间模式, 只是融合通道。

![../_images/conv-1x1.svg](https://zh.d2l.ai/_images/conv-1x1.svg)



### 二维卷积层的参数

- 输入 $\mathbf{X}: c_i \times n_h \times n_w$
- 核 $\mathbf{W}: c_o \times c_i \times k_h \times k_w$
- 偏差 $\mathbf{B}: c_o \times c_i$
- 输出 $\mathbf{Y}: c_o \times m_h \times m_w$

## 池化/汇聚层 (Pooling)

- 使用池化层的理由：卷积对位置敏感，需要降低卷积层对位置的敏感性、降低对空间降采样表示的敏感性
    - 在检测垂直边缘不好，1像素移位就可能导致 0 输出

- 池化层返回窗口中最大或平均值
- 缓解卷积层对位置的敏感性
- 同样有窗口大小、填充、和步幅作为超参数

### 二维最大池化

- 直接返回滑动窗口中的最大值
- 最大池化层: 每个窗口中最强的模式信号

![../_images/pooling.svg](https://zh.d2l.ai/_images/pooling.svg)


$$
\max (0,1,3,4)=4
$$


### 平均池化层

- 平均池化层：将最大池化层中的 “最大” 操作替换为 “平均”

## LeNet

总体来看，LeNet（LeNet-5）由两个部分组成：

- 卷积编码器：由两个卷积层组成
- 全连接层密集块：由三个全连接层组成

![../_images/lenet.svg](https://zh.d2l.ai/_images/lenet.svg)

[^1]: LeNet中的数据流。输入是手写数字，输出为10种可能结果的概率

![../_images/lenet-vert.svg](https://zh.d2l.ai/_images/lenet-vert.svg)

## AlexNet

![../_images/alexnet.svg](https://zh.d2l.ai/_images/alexnet.svg)

[^]: 从LeNet（左）到AlexNet（右）

