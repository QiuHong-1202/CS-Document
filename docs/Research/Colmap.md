# Colmap

## Multi View Stereo

- Current MVS pipeline for 3D reconstruction (2 stages)
    - Estimating the **depth map** for each image based on MVS
    - Performing **depth fusion** to obtain the final reconstruction result

> MVS downstream application
>
> - novel view synthesis



## Incremental & global SFM

- **Incremental SFM**
    - 首先从一张或几张图像中恢复出初始的三维结构和摄像机参数。然后，每次引入一张新图像时，系统会将该图像与先前已恢复的模型进行比较，计算新图像中特征点与已知三维点的对应关系，并使用这些对应关系来优化摄像机参数和三维点的位置。这个过程不断迭代，每次处理一张新图像，逐步完善场景模型。
    - Pros: 适用于处理大规模图像序列、能够实时地更新模型
    - Cons: 每次迭代只考虑局部信息，可能会导致积累误差

- **Global SFM**
    - 同时考虑整个图像序列，系统会在整个图像序列中寻找共同的特征点并且同时优化所有的摄像机参数和三维点位置，以最大程度地减小整个场景模型的重投影误差。这种方法通常使用大规模非线性优化算法来解决
    - Pros: 可以更准确地建立整个场景的三维模型，因为它考虑了所有的图像和特征点信息，从而减小了累积误差的影响
    - Cons: 需要处理整个图像序列，全局式结构光通常计算复杂度较高，可能不适用于实时应用或大规模场景



## Colmap SFM pipeline

![Incremental Structure-from-Motion pipeline](https://colmap.github.io/_images/incremental-sfm.png)

### Overview

- SFM 通常首先进行**特征提取/匹配**以及后续的**几何校验**滤出外点，经过上述步骤可以得到所谓的场景图（Scene Graph），该场景图是后续的增量式的基础（提供数据关联等信息）

- 增量式重建中需要非常仔细地挑选两帧进行重建，在图像进行注册（即定位当前帧在地图中的位姿）之前，需要进行三角化场景点/滤出外点以及 **BA 优化**当前的模型

### Correspondence Search

输入：一系列图片；输出：经过几何校验后的图像匹配关系。

为了得到尽可能准确的匹配关系，该步骤中涉及特征提取，匹配以及几何校验。

- 特征匹配：可以是任何一种特异性较强的特征，如 SIFT（COLMAP默认用SIFT），主要为后续的特征匹配服务
- 匹配阶段，将输入的图像两两之间进行匹配（可以发现，这一步的时间复杂度非常大），得到潜在的场景重合部分
- 几何校验：初始匹配的外点势必很多，此时需要滤出外点。通常情况下会用到基础矩阵（未标定）/本质矩阵（已标定）以及单应矩阵（纯旋转/共面）。图像经过上述三个步骤之后的输出为 **scene graph**，即图像是节点，几何校验后的匹配对是边。



>- 外点（Outliers）：在特征匹配过程中被错误地匹配的点或特征
>- 内点（Inliers）：内点指的是在特征匹配过程中被正确地匹配的点或特征

### Incremental Reconstruction

输入：**scene graph**；输出：相机位姿以及3D路标点；

为了完成增量重建，需要完成初始化，图像注册，三角化以及BA优化这些步骤。

- 初始化：SfM在初始化时需要非常仔细的选择两帧进行重建；此时需要尽量选择**scene graph**中相机间可视区域多的两视角进行初始化，文中称这种选择增加了“redundancy”进而增加了重建的鲁棒性与精确性。
- 图像注册：即根据已有的SfM模型估计图片的位姿（更准确的是估计拍摄该图像相机的位姿）；根据未知的图像与地图中图像的2D-2D匹配，进而得到二者之间的2D-3D匹配，然后利用RANSAC-PNP解算出该相机位姿，完成图像注册。为了提高位姿解算精度以及可靠的三角化，本文设计了新颖的鲁棒后续帧选择策略，后续章节进行介绍。
- 三角化：新注册的图像需要对已有的场景点有足够多的观测，同时也可以通过三角化扩展场景点。现有的三角化方法鲁棒性不足且耗时严重。本文设计了一种全新的三角化策略，后续章节进行介绍。
- BA 优化：由于图像注册与三角化是分开进行的，但二者是强相关的两个过程：错误的位姿会导致错误的三角化点点产生，反之亦然。BA 能够同时优化相机位姿以及地图点，使模型的 redundancy 更强。优化目标是通过调整相机位姿与地图点位置使重投影误差最小


$$
E=\sum_j \rho_j\left(\left\|\pi\left(\mathbf{P}_c, \mathbf{X}_k\right)-\mathbf{x}_j\right\|_2^2\right)
$$


BA问题通常可以通过LM算法进行求解。但是，当SfM面对网络图像时，特别对于那些几乎一样的图像时，上述优化过程会占用极长的时间。



> - 位姿：拍摄图像的相机在三维空间中d

## Algorithm Detail

### Scale-invariant feature transform (SIFT)

- SIFT 算法的实质是在不同的尺度空间上查找关键点(特征点)，并计算出关键点的方向。
    - P.S. SIFT 所查找到的关键点是一些十分突出，不会因光照，仿射变换和噪音等因素而变化的点，如角点、边缘点、暗区的亮点及亮区的暗点等
- 4 steps of SIFT
    - 尺度空间极值检测：搜索所有尺度上的图像位置。通过高斯微分函数来识别潜在的对于尺度和旋转不变的兴趣点
    - 关键点定位：在每个候选的位置上，通过一个拟合精细的模型来确定位置和尺度。关键点的选择依据于它们的稳定程度
    - 方向确定：基于图像局部的梯度方向，分配给每个关键点位置一个或多个方向。所有后面的对图像数据的操作都相对于关键点的方向、尺度和位置进行变换，从而提供对于这些变换的不变性
    - 关键点描述：在每个关键点周围的邻域内，在选定的尺度上测量图像局部的梯度。这些梯度被变换成一种表示，这种表示允许比较大的局部形状的变形和光照变化

### Matching



### Geometric verification

- [ ] RANSAC
- [ ] 基础矩阵（未标定）/本质矩阵（已标定）以及单应矩阵（纯旋转/共面）



### Initialization



### Image Registration



### Triangulation



### Bundle Adjustment





## Reference Links

- [三维重建系列 COLMAP: Structure-from-Motion Revisited](https://vincentqin.tech/posts/colmap/)