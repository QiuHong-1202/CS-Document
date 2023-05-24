## 梯度

我们可以连结一个多元函数对其所有变量的偏导数, 以得到该函数的梯度 (gradient) 向量。具体而言, 设函数 $f: \mathbb{R}^n \rightarrow \mathbb{R}$ 的输入是 $一$ 个 $n$ 维向量 $\mathbf{x}=\left[x_1, x_2, \ldots, x_n\right]^{\top}$, 并且输出是一个标量。函数 $f(\mathbf{x})$ 相对于 $\mathbf{x}$ 的梯度是一个包含 $n$ 个偏导数的向量:



$$
\nabla_{\mathbf{x}} f(\mathbf{x})=\left[\frac{\partial f(\mathbf{x})}{\partial x_1}, \frac{\partial f(\mathbf{x})}{\partial x_2}, \ldots, \frac{\partial f(\mathbf{x})}{\partial x_n}\right]^{\top}
$$



其中 $\nabla_{\mathbf{x}} f(\mathbf{x})$ 通常在没有歧义时被 $\nabla f(\mathbf{x})$ 取代。

假设 $\mathrm{x}$ 为 $n$ 维向量, 在微分多元函数时经常使用以下规则:

- 对于所有 $\mathbf{A} \in \mathbb{R}^{m \times n}$, 都有 $\nabla_{\mathbf{x}} \mathbf{A} \mathbf{x}=\mathbf{A}^{\top}$
- 对于所有 $\mathbf{A} \in \mathbb{R}^{n \times m}$, 都有 $\nabla_{\mathbf{x}} \mathbf{x}^{\top} \mathbf{A}=\mathbf{A}$
- 对于所有 $\mathbf{A} \in \mathbb{R}^{n \times n}$, 都有 $\nabla_{\mathbf{x}} \mathbf{x}^{\top} \mathbf{A} \mathbf{x}=\left(\mathbf{A}+\mathbf{A}^{\top}\right) \mathbf{x}$
- $\nabla_{\mathbf{x}}\|\mathbf{x}\|^2=\nabla_{\mathbf{x}} \mathbf{x}^{\top} \mathbf{x}=2 \mathbf{x}$  ([P.S. Vector derivation of $x^Tx$](https://math.stackexchange.com/questions/132415/vector-derivation-of-xtx))

同样, 对于任何矩阵 $\mathbf{X}$, 都有 $\nabla_{\mathbf{X}}\|\mathbf{X}\|_F^2=2 \mathbf{X}$ 。

## 线性模型

### 线性模型的实例

考虑一个房屋的价格的线性假设 [P.S. 指目标（房屋价格）可以表示为特征（面积和房龄）的加权和] 


$$
\text { price }=w_{\text {area }} \cdot \text { area }+w_{\text {age }} \cdot \text { age }+b
$$



- 上式中的 $w_{\text {area }}$ 和 $w_{\text {age }}$ 称为权重（weight），权重决定了每个特征对我们预测值的影响。 
- $b$ 称为偏置（bias）、偏移量（offset） 或截距 (intercept)。 偏置是指当所有特征都取值为 $0$ 时, 预测值应该为多少。
  - 即使现实中不会有任何房子的面积是 0 或房龄正好是 0 年, 我们仍然需要偏置项。如果没有偏置项, 我们模型的表达能力将受到限制。
- 严格来说，上式是输入特征的一个仿射变换 (affine transformation）。仿射变换的特点是通过加权和对特征进行线性变换（linear transformation），并通过偏置项来进行平移 (translation)。

### 抽象的线性模型

对于 $n$ 维输入 $[x_1,x_2...x_n]^T$，线性模型有 $n$ 维权重 $[w_1,w_2...w_n]^T$ 和一个标量偏差 $b$

当输入包含 $d$ 个特征时，预测结果 $\hat{y}$ 可以表示为


$$
\hat{y}=w_1 x_1+\ldots+w_d x_d+b
$$



[向量版本] 将所有特征放到向量 $\mathbf{x} \in \mathbb{R}^d$ 中, 并将所有权重放到向量 $\mathbf{w} \in \mathbb{R}^d$ 中, 我们可以用点积形式来简洁地表达模型：


$$
\hat{y}=\mathbf{w}^{\top} \mathbf{x}+b .
$$



> 下面将通过这个例子描述概念

## 损失函数

- 衡量预估质量的指标，越小越好
- 通过比较真实值和预估值的方式实现，例如房屋的实际售价和估价
- e.g. 假设 $y$ 是真实值，$\hat{y}$ 是估计值，我们可以比较


$$
\ell(y, \hat{y})=\frac{1}{2}(y-\hat{y})^2
$$

>- 这就是平方损失
>
>- 常数 $\frac{1}{2}$ 不会带来本质的差别，但这样在形式上稍微简单一些 （因为当我们对损失函数求导后常数系数为1）

## 训练数据

- 收集一些数据点来决定参数值（权重 $w$ 和偏差 $b$）
- 这就是训练数据，通常越多越好
- 假设我们有 $n$ 个样本，记 $X=[x_1,x_2...x_n]^T, y=[y_1,y_2...y_n]^T$ 

## 参数学习

- 训练损失：就是对每一个数据上的损失求一个均值

$$
\ell(X,y,w,b)=\frac{1}{2}\times \frac{1}{n}\sum_{i=1}^{n}(y_i-\hat{y_i})^2 = \frac{1}{2n}\sum_{i=1}^{n}(y_i-<x_i,w>-b)^2
$$

写成向量形式为


$$
\frac{1}{2n}||y-Xw-b||^2
$$


- 训练目标：找到 $w,b$ ，使得 $\ell(X,y,w,b)$ 是最小的，可以写成如下形式


$$
w^*,b^*=\arg{\min_{w,b}{\ell(X,y,w,b)}}
$$

线性模型是存在解析解的，我们可以直接求出线性模型的最优解。在求解时，为了方便起见，我们将偏差 $b$ 加入权重 $w$ 的矩阵中，使其成为一个特征，对于矩阵 $X$，就添加一个全 $1$ 的列来保证二者相乘是有效的，于是


$$
\ell(X,y,w,b)=\ell(X,y,w') = \frac{1}{2n}||y-Xw||^2
$$


由于这是一个凸函数，最小值在梯度为 $0$ 时取到，因此令


$$
\frac{\partial{\ell(X,y,w)}}{\partial{w}}=\frac{1}{n}(y-Xw)^TX= 0
$$


解上式有


$$
\frac{1}{n}(y-Xw)^TX=0\\
y^TX-(w^TX^T)X=0\\
w^T=y^TX(X^TX)^{-1}\\
$$


于是


$$
\begin{aligned}
 w &= [y^TX(X^TX)^{-1}]^T &\\
 &=[(y^TX)(X^TX)^{-1}]^T&\\
 &=[(X^TX)^{-1}]^T(y^TX)^T&\\
 &=[(X^TX)^{T}]^{-1}(y^TX)^T&\\
 &=(X^TX)^{-1}(X^Ty)&
\end{aligned}
$$



## 基本优化方法

如果不采用解析做法，或者模型无法使用解析方法求解的时候，需要使用优化的方法来求解

### 梯度下降

在求解参数的时候，对于参数 $w$，对其赋予一个随机初值 $w_0$，在规定的步数 $t = t_1,t_2,t_3,...,t_n$ 内，更新 $w_{t_i}$ 的值。并且，$w_{t}$ 和 $w_{t-1}$ 之间有如下关系


$$
w_t = w_{t-1} - \eta\frac{\partial{\ell}}{\partial{w_{t-1}}}
$$


- $\eta$ 是学习率，也就是每一次梯度下降的步长，它是一个超参数
  - 注意：计算梯度的开销是很大的，在选择学习率时要选择一个合适的值

> 超参数：人为指定的值

### 小批量随机梯度下降

由于计算全部样本的梯度开销还是太大，所以采用随机采样 $b$ 个样本 $i_1,i_2,...,i_b$  的方法来近似损失，$b$ 的值叫做 batch size，它也是一个超参数，小批量随机采样的损失为


$$
\frac{1}{b}\sum_{i\in I_b}\ell(x_i,y_i,w)
$$
