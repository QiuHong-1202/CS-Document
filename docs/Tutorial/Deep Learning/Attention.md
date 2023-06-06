# Attention

## Attention Mechanism

- 注意力机制的心理学框架：人类根据随意线索和不随意线索来选择注意点
  - 随意线索：根据人类主观想法的事物（想读书）
  - 不随意线索：不根据人类主观想法的线索（眼睛注意到的红色杯子）
- 卷积、全连接、池化都只考虑不随意线索
- 注意力机制则**显式的**考虑随意线索
  - 随意线索被称之为查询（query）
  - 每一个输入是一个值（value）和不随意线索（key）的对
  - 通过注意力池化层根据 ***query*** 来有偏向性的选择某些输入
  - 可以一般的写作 $f(x)=\sum_i \alpha(x, x_i) y_i$, 这里 $\alpha\left(x, x_i\right)$ 是注意力权重

### 非参注意力池化层

- 给定数据 $(x_i,y_i), i=1,...,n$
- 平均池化（$x$ 为 query）：$f(x)=\frac{1}{n}\sum_iy_i$
- Nadaraya-Watson 核回归：
  - $x$ 为 query
  - $x_i, x_j$ 为 key
  - $y_i$ 为 value
  - $K(x-x_i)$ 为核（kernel），衡量 $x$ 和 $x_i$ 之间距离的函数，会选择和离 $x$ 比较近的 $x_i$
  - 变成概率后每一项 $y_i$ 就是它的相对重要性


$$
f(x)=\sum_{i=1}^n\frac{K(x-x_i)}{\sum_{j=1}^nK(x-x_j)}y_i
$$


如果使用高斯核 $K(u)=\frac{1}{\sqrt{2 \pi}} \exp \left(-\frac{u^2}{2}\right)$ ，那么


$$
\begin{aligned}
f(x) & =\sum_{i=1}^n \frac{\exp \left(-\frac{1}{2}\left(x-x_i\right)^2\right)}{\sum_{j=1}^n \exp \left(-\frac{1}{2}\left(x-x_j\right)^2\right)} y_i \\
& =\sum_{i=1}^n \operatorname{softmax}\left(-\frac{1}{2}\left(x-x_i\right)^2\right) y_i
\end{aligned}
$$




### 参数化的注意力机制

- 在之前的基础上引入可以学习的 $w$ （此处为标量）


$$
f(x)=\sum_{i=1}^n \operatorname{softmax}\left(-\frac{1}{2}\left(\left(x-x_i\right) w\right)^2\right) y_i
$$


## 注意力分数

