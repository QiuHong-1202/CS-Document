# 3D Scene Analysis

!!! note

    start on: Aug 23, 2023



## Principal of Indoor Scene Network Design

> From the talk of Richard in 2023/9/3

### Description

- function description
- structural description
    - object parts
    - part relations

### 3C Principal

- consistency
    - weak prior: same class = same function
    - e.g. cycle consistency (for unpaired domain translation)
    - e.g. VAE (predictable & compressibility $\to$ need redundancy [*symmetry*] )
        - bottle neck layer in neural network: force to compress
- compactness
    - model representation
- continuity
    - linkage between the scene (bridge gap)



## Related Algorithm

### Signed distance field

- signed distance from the edge of a shape
    - inside shape: negative
    - outside shape: positive
    - exactly on the shape: 0

![image-20230824152525493](./assets/image-20230824152525493.png)

### Marching Cube

> - [游戏编程挑战：生成无边的水下世界 体绘制算法 | Coding Adventure: Marching Cubes](https://www.bilibili.com/video/BV1yJ411r73v/)

使用 3D 空间中的一个点作为输入， 随后返回一个值


$$
f(x,y,z) \to v
$$


假设在空间中的某个区域内，我们可以使用函数 $f$ 等间距的采样一些点

不妨设函数 $f$ 的最大值为 $16$，最小值为 $-32$，如果存在一个表面阈值 $sf$，当表面阈值从 $-32$ 增长到 $16$ 时，均匀采样点就会逐渐消失（视频 0:45）

我们可以认为消失的点是空白的空间，而大于等于表面阈值的点，则处于形体的表面或者内部

如果把这个问题简化到一个立方体内部，如果白色的点位于物体内部，它就被激活，这样我们就得到了一个三角面片



![image-20230828102922879](./assets/image-20230828102922879.png)



## Useful Links

- [Camera Sensor Size](https://designreviews.com/digital-camera-sensor-size-chart/)
- [体渲染 (Volume Rendering)](https://zhuanlan.zhihu.com/p/595117334)