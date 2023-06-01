# LaTeX

## 数集符

| 中文名称 |   渲染前   |    渲染后    |
| :------: | :--------: | :----------: |
|  自然数  | \mathbb{N} | $\mathbb{N}$ |
|   实数   | \mathbb{R} | $\mathbb{R}$ |
|   整数   | \mathbb{Z} | $\mathbb{Z}$ |
|  有理数  | \mathbb{Q} | $\mathbb{Q}$ |

## 运算符

### 简单运算符

|        中文名称         | 渲染前 |  渲染后  |
| :---------------------: | :----: | :------: |
|           加            |   +    |   $+$    |
|           减            |   -    |   $-$    |
|           乘            | \times | $\times$ |
|           除            |  \div  |  $\div$  |
|          点乘           | \cdot  | $\cdot$  |
|           交            |  \cap  |  $\cap$  |
|           并            |  \cup  |  $\cup$  |
|          加减           |  \pm   |  $\pm$   |
|          减加           |  \mp   |  $\mp$   |
| Nabla算子/梯度/向量微分 | \nabla | $\nabla$ |

### 大型运算符

| 中文名称 |         渲染前(源码)          |             渲染后              |
| :------: | :---------------------------: | :-----------------------------: |
|   求和   |         \sum_{i=1}^n          |         $\sum_{i=1}^n$          |
|   求积   |         \prod_{i=1}^n         |         $\prod_{i=1}^n$         |
|   积分   |      \int_{0}^{+\infty}       |      $\int_{0}^{+\infty}$       |
|  求偏导  | \frac{\partial f}{\partial x} | $\frac{\partial f}{\partial x}$ |

## 关系符

P.S. 如无特殊说明下面的关系符的否定形式都为肯定形式的源码前加上 `not`

| 中文名称 |   渲染前    |   渲染后    |
| :------: | :---------: | :---------: |
|   小于   |      <      |     $<$     |
|   大于   |      >      |     $>$     |
|   等于   |      =      |     $=$     |
|  不等于  |    \neq     |   $\neq$    |
|  约等于  |   \approx   |  $\approx$  |
|   同余   |   \equiv    |  $\equiv$   |
| 小于等于 | \le 或 \leq |    $\le$    |
| 大于等于 | \ge 或 \geq |    $\ge$    |
|   属于   |     \in     |    $\in$    |
|   含于   |  \subseteq  | $\subseteq$ |
|   整除   |    \mid     |   $\mid$    |

## 希腊字母

### 小写字母

|   渲染前    |    渲染后     |
| :---------: | :-----------: |
|   \alpha    |   $\alpha$    |
|    \beta    |    $\beta$    |
|   \gamma    |   $\gamma$    |
|   \theta    |   $\theta$    |
|   \lambda   |   $\lambda$   |
|     \mu     |     $\mu$     |
|     \xi     |     $\xi$     |
|    \rho     |    $\rho$     |
|   \varphi   |   $\varphi$   |
|   \omega    |   $\omega$    |
| \varepsilon | $\varepsilon$ |
|   \sigma    |   $\sigma$    |
|    \eta     |    $\eta$     |
|    \ell     |    $\ell$     |

### 大写字母

将小写形式源码的第一个字符大写

| 渲染前 |  渲染后  |
| :----: | :------: |
| \Sigma | $\Sigma$ |
|  \Pi   |  $\Pi$   |
| \Delta | $\Delta$ |

## 格式符号

### 点点

| 渲染前 |  渲染后  |
| :----: | :------: |
| \cdot  | $\cdot$  |
| \cdots | $\cdots$ |
| \vdots | $\vdots$ |
| \ddots | $\ddots$ |
| \ldots | $\ldots$ |

### 空格

|   渲染前    |   渲染后    |
| :---------: | :---------: |
|   `a\!b`    |   $a\!b$    |
|    `ab`     |    $ab$     |
|   `a\,b`    |   $a\,b$    |
|   `a\;b`    |   $a\;b$    |
|   `a\ b`    |   $a\ b$    |
| `a\quad b`  | $a\quad b$  |
| `a\qquad b` | $a\qquad b$ |

### 括号

| 中文名称 |      渲染前       |         渲染后          |
| :------: | :---------------: | :---------------------: |
|  小括号  |        ()         |          $()$           |
|  中括号  |        []         |          $[]$           |
|  大括号  |      `\{\}`       |         $\{\}$          |
|  下取整  | `\lfloor \rfloor` | $\lfloor\theta \rfloor$ |
|  上取整  |  `\lceil \rceil`  | $\lceil \theta \rceil$  |

### 箭头

命名规则为，方向+箭头种类

|       渲染前        |    渲染后     |
| :-----------------: | :-----------: |
| \leftarrow 或 \gets | $\leftarrow$  |
| \rightarrow 或 \to  | $\rightarrow$ |
|      \uparrow       |  $\uparrow$   |

四个基本方向为上下左右，斜着的箭头的方向部分为 `\ne \se \nw \sw`，为东北、东南、西北、西南简写

e.g. `\nearrow`: $\nearrow$

左右、上下两个方向的箭头

|     渲染前      |      渲染后       |
| :-------------: | :---------------: |
| \leftrightarrow | $\leftrightarrow$ |
|  \updownarrow   |  $\updownarrow$   |

可以通过大写第一个字母变成双线

|     渲染前      |      渲染后       |
| :-------------: | :---------------: |
| \Leftrightarrow | $\Leftrightarrow$ |
|  \Updownarrow   |  $\Updownarrow$   |

在前面加上`long`可以把箭头变长，仅适用于左右箭头

|                渲染前                |        渲染后         |
| :----------------------------------: | :-------------------: |
|            \longleftarrow            |   $\longleftarrow$    |
|         \longleftrightarrow          | $\longleftrightarrow$ |
| \Longleftrightarrow 或 \iff (等价于) |        $\iff$         |

只有一边的箭头，名字为harpoon+up/down，表示那一边的位置

|       渲染前       |        渲染后        |
| :----------------: | :------------------: |
|   \leftharpoonup   |   $\leftharpoonup$   |
| \rightleftharpoons | $\rightleftharpoons$ |

### 其他

| 中文名称 |      渲染前      |    渲染后    |
| :------: | :--------------: | :----------: |
|    度    |      \circ       |   $\circ$    |
|   无穷   |      \infty      |   $\infty$   |
|   空集   |    \emptyset     | $\emptyset$  |
| ...到... |       \sim       |    $\sim$    |
|    角    |      \angle      |   $\angle$   |
|   对数   |       \log       |    $\log$    |
|  下划线  |       `\_`       |     $\_$     |
|    模    |      \mod x      |   $\mod x$   |
|  换行符  | `\\` 或 \newline |              |
|   因为   |     \because     |  $\because$  |
|   所以   |    \therefore    | $\therefore$ |
|   存在   |     \exists      |  $\exists$   |
|   任意   |     \forall      |  $\forall$   |

## 语法

### 根式

大括号定界，基本用法如下：


$$
\text{\\sqrt\{x\}} \to \sqrt{x}
$$


可以在大括号前面添加方括号，方括号里为开根的次数


$$
\text{\\sqrt[5]\{x\}} \to \sqrt[5]{x}
$$


符号大小自动调整，支持嵌套，方括号与大括号内的内容无特殊限制.

特殊的，可以不显示上方的横线：


$$
\text{\\surd\{x\}} \to \surd{x}
$$


### 上/下标

- 源码（渲染前）

```
x_{1+2_i}^{999^2}
```

- 渲染后

$$
x_{1+2_i}^{999^2}
$$

支持多重嵌套，当没有大括号时默认渲染后面第一个字符.



### 上/下划线



| 中文名称 |              渲染前               |               渲染后                |
| :------: | :-------------------------------: | :---------------------------------: |
|  上划线  |          \overline{a+b}           |          $\overline{a+b}$           |
|  下划线  |          \underline{a+b}          |          $\underline{a+b}$          |
|   嵌套   | \overline{\underline{\sqrt{a+b}}} | $\overline{\underline{\sqrt{a+b}}}$ |



### 上/下括号

|   中文名称   |         渲染前         |          渲染后           |
| :----------: | :--------------------: | :-----------------------: |
| 单独的上括号 | \overbrace{0\cdots 0}  | $\overbrace{0 \cdots 0}$  |
| 单独的下括号 | \underbrace{0\cdots 0} | $\underbrace{0 \cdots 0}$ |


也可以为括起来的部分加上文字，上括号用 `^`，下括号用 `_`

|   中文名称   |                      渲染前                      |                       渲染后                       |
| :----------: | :----------------------------------------------: | :------------------------------------------------: |
| 上括号加文字 |           \overbrace{0\cdots 0}^{n个0}           |           $\overbrace{0\cdots 0}^{n个0}$           |
| 下括号加文字 |          \underbrace{0\cdots 0}_{n个0}           |          $\underbrace{0\cdots 0}_{n个0}$           |
| 上下括号嵌套 | \underbrace{\overbrace{0\cdots 0}^{n个0}}_{n个0} | $\underbrace{\overbrace{0\cdots 0}^{n个0}}_{n个0}$ |

### 向量

|                描述                |       渲染前       |        渲染后        |
| :--------------------------------: | :----------------: | :------------------: |
|              直接定义              |   \vec {abcdas}    |   $\vec {abcdas}$    |
| 在上方加箭头的语法来达到向量的效果 | \overrightarrow{a} | $\overrightarrow{a}$ |

### 分数

|   描述   |      渲染前      |       渲染后       |
| :------: | :--------------: | :----------------: |
| 直接定义 | \frac{x^8}{4132} | $\frac{x^8}{4132}$ |

### 组合数

|   描述   |      渲染前      |       渲染后       |
| :------: | :--------------: | :----------------: |
| 直接定义 | \binom{233}{x^2} | $\binom{233}{x^2}$ |

### 对齐

用 `&` 来对齐公式，每行的 `&` 从左到右依次对齐，`&` 的个数不同会让对齐时公式块略有偏移

```
\begin{aligned}
 f(x) &= (x+a)(x+b) &(1)\\
 &= x^2 + (a+b)x + ab&&(2)\\
 &=x\times x + ax+bx+ab&(3)
\end{aligned}
```


$$
\begin{aligned}
 f(x) &= (x+a)(x+b) &(1)\\
 &= x^2 + (a+b)x + ab&&(2)\\
 &=x\times x + ax+bx+ab&(3)
\end{aligned}
$$


居中的话直接在两个 `$$` 之间写，默认居中。

### 大括号表达式

前后加一行，中间在 `aligned` 环境里写表达式，依然可以用 `&` 对齐表达式或者表达式的部分 

```
\left\{
\begin{aligned}
&a=b+c\\
&c=x
\end{aligned}
\right.
```


$$
\left\{
\begin{aligned}
&a=b+c\\
&c=x
\end{aligned}
\right.
$$


更多用法，将限制写在 `&&` 后面，用大括号定界，可以左对齐，只用单个 `&` 是右对齐：

- 左对齐

```
f(T)=\left\{
\begin{aligned}
&\mu(1)&&{T\in P}\\
&\mu(i)&&{i \mod\ p[j]=0}\\
&-f(i)+\mu(i)&&{i \mod\ p[j]\ne 0}
\end{aligned}
\right.
```


$$
f(T)=\left\{
\begin{aligned}
&\mu(1)&&{T\in P}\\
&\mu(i)&&{i \mod\ p[j]=0}\\
&-f(i)+\mu(i)&&{i \mod\ p[j]\ne 0}
\end{aligned}
\right.
$$


- 右对齐

```
f(T)=\left\{
\begin{aligned}
&\mu(1)&{T\in P}\\
&\mu(i)&{i \mod\ p[j]=0}\\
&-f(i)+\mu(i)&{i \mod\ p[j]\ne 0}
\end{aligned}
\right.
```


$$
f(T)=\left\{
\begin{aligned}
&\mu(1)&{T\in P}\\
&\mu(i)&{i \mod\ p[j]=0}\\
&-f(i)+\mu(i)&{i \mod\ p[j]\ne 0}
\end{aligned}
\right.
$$


### 矩阵

利用 `\begin{array}{l}`（ `{l}` 为对齐方式）与 `\end{array}` 环境，中间写表格内容，用 `&` 划分列， `\\` 划分行.

```
\left[\begin{array}{l}
a & b\\
c & d\\
\end{array}
\right]
```

其中 `\left` + 左括号是为了给一个可以自适应大小的左括号，样式自选，右括号同理，效果如下：


$$
\left[\begin{array}{l}
a & b\\
c & d\\
\end{array}
\right]
$$


把括号拆了还可以用来写表达式：


$$
\begin{array}{l}
y=x+1 & x<0\\
y=x-1 & x>0\\
\end{array}
$$
