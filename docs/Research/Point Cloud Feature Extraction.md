# Point Cloud Feature Extraction

## PointNet

## PointNet++

## Dynamic Graph CNN

- 假设一个 $F$ 维点云有 $n$ 个点，定义为: $X=x_1, \ldots, x_n \in R^F$ 
    - 最简单地情况下， $F=3$ ，三维坐标。
    - 更一般的情况下，额外的信息可能增高维度，例如颜色、表面法线等
    - 在一个深度神经网络中，后面的层都会接受前一层的输出，因此更一般的情况下，维度 $F$ 也可以表示某一层的特征维度



- 假设给定一个有向图 $G=(v, e)$ ，用来表示点云的局部结构，其中顶点为 $v=\{1, \ldots, n\}$ ，而边则为 $e \in v \times v$ 
- 在最简单的情况下，我们建立一个 KNN 图 $G$
    - 假设距离点 $x_i$ 最近的点 $x_{j_{i 1}}, \ldots, x_{j_{i k}}$ 
    - 包含许多有向边缘 $\left(i, j_{i 1}\right), \ldots,\left(i, j_{i k}\right)$ 
- 我们定义边缘特征为: $e_{i j}=h_{\Theta}\left(x_i, x_j\right)$ ，其中 $h_{\Theta}: \mathbb{R}^F \times \mathbb{R}^F \rightarrow \mathbb{R}^{F^{\prime}}$ ，是一些使用一些可学习的参数 $\Theta$ 构成的非线性函数



- 最后在 EdgeConv 操作上添加一个通道级的对称聚合操作 $\square$ 


$$
x_i^{\prime}=\square_{j:(i, j) \in \epsilon} h_{\Theta}\left(x_i, x_j\right)
$$


- 关于公式中的 $h$ 和 $\square$ 有四种可能的选择:

1. $h_{\Theta}\left(x_i, x_j\right)=\theta_j x_j$ ，聚合操作采用求和操作: $x_i^{\prime}=\sum_{j:(i, j) \in \epsilon} \theta_j x_j$ 
2. $h_{\Theta}\left(x_i, x_j\right)=h_{\Theta}\left(x_i\right)$ ，只提取全局形状信息，而忽视了局部领域结构。这类网络实际上就是 PointNet，因此 PointNet 中可以说 使用了特殊的 EdgeConv 模块
3. $h_{\Theta}\left(x_i, x_j\right)=h_{\Theta}\left(x_j-x_i\right)$ 。这种方式只对局部信息进行编码，在本质上就是将原始点云看做一系列小块的集合，丢失了原始 的全局形状结构信息
4. 文中采用的， $h_{\Theta}\left(x_i, x_j\right)=h_{\Theta}\left(x_i, x_j-x_i\right)$ ，这样的结构同时结合了全局形状信息以及局部领域信息




