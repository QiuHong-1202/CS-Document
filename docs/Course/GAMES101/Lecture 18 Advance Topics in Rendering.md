# Lecture 18 Advance Topics in Rendering

## Advanced Light Transport

### Advanced Light Transport

- Unbiased light transport methods
  - Bidirectional path tracing (BDPT)
  - Metropolis light transport (MLT)
- Biased light transport methods
  - Photon mapping
  - Vertex connection and merging (VCM)
- Instant radiosity (VPL / many light methods)

### Biased vs. Unbiased Monte Carlo Estimators

- An **unbiased** Monte Carlo technique does not have any systematic error
  - The expected value of an unbiased estimator will always be the correct value, no matter how many samples are used
  - 估计出的结果的期望永远都是我们要的真实值
- Otherwise, **biased**
  - One **special case**, the expected value converges to the correct value as infinite \#samples are used - **consistent**
  - 估计出的结果的期望和真实值不同
- An easier understanding bias in rendering 
  - **Biased** == blurry 
  - **Consistent** == not blurry with infinite #samples

### Bidirectional Path Tracing (BDPT)

- Name: 双向路径追踪
- Recall: a path connects the camera and the light （生成一些半路径）
  - Traces sub-paths from both the camera and the light 
  - Connects the end points from both sub-paths

- Pros
  - Suitable if the light transport is complex on the light’s side
  - unbiased
- Cons
  - **Difficult to implement** 
  - quite **slow**

![image-20221121154154021](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211542157.png)

- 双向路径追踪好的原因：因为对于这个场景而言，从摄像机出发做 Path Tracing 第一个打到的地方是 diffuse 的表面，这就导致了之后的路径不容易到达能量集中的区域
- 而双向路径追踪适用于光线在光源处容易算的情况

### Metropolis Light Transport (MLT)

- 思想：使用统计学上的马克可夫链（根据当前的样本生成一个和它靠近的下一个样本）做采样工具
- A Markov Chain Monte Carlo (MCMC) application 
  - Jumping from the current sample to the next with some PDF 
- Very good at **locally** exploring difficult light paths
- Key idea: Locally **perturb an existing path to get a new path**

![image-20221121154954427](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211549456.png)

- Pros
  - Works great with difficult light paths 
    - 找到一条光线作为种子，可以在它周围找到其他的光线
  - unbiased
- Cons
  - Difficult to estimate the convergence rate （收敛速率，也就是渲染速度难以分析）
  - Does not guarantee equal convergence rate per pixel 
    -  usually produces “dirty” results
    - usually not used to render animations

![image-20221121155254390](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211552474.png)

![image-20221121155511449](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211555533.png)

### Photon Mapping

- A biased approach & A two-stage method 
- Very good at handling **Specular-Diffuse-Specular (SDS) paths** and generating caustics
  - caustics: 由于光线的聚焦产生的非常强的一些图案，例如水面的波纹

#### Approach (variations apply)

- Stage 1 — photon tracing
  - Emitting photons from the light source, bouncing them around, then recording photons on diffuse surfaces（当光子打到 diffuse 的物体后停下）

![image-20221121160259096](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211602119.png)

- Stage 2 — photon collection (final gathering)
  - Shoot **sub-paths** from the camera, bouncing them around, until they hit diffuse surfaces （当 sub-paths 打到 diffuse 的物体后停下）
- Calculation — local density estimation
  - Idea: areas with more photons should be brighter 
  - For **each shading point**, find the nearest $N$ photons. Take the **surface area** they over
  - 计算光子的密度

![image-20221121160134287](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211601318.png)

#### Why biased?

- Local Density estimation $dN / dA \ne ΔN / ΔA$
- But in the sense of limit
  - More photons emitted $\to$ the same $N$ photons covers a smaller $ΔA$ $\to$ $ΔA$ is closer to $dA$ （So, biased but consistent!）
- Why not do a “const range” search for density estimation?
  - More photons emitted $\to$ in the same const range will have more photons $\to$ $ΔA$ is not closer to $dA$ （So, biased and not consistent!）

### Vertex Connection and Merging

- 结合双向路径追踪和光子映射
- Key idea
  - Let’s not waste the sub-paths in BDPT if their end points cannot be connected but can be merged
  - Use photon mapping to handle the merging of nearby “photons”

![image-20221121161242955](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211612981.png)

### Instant Radiosity (IR)

- Sometimes also called many-light approaches
- Key idea
  - Lit surfaces can be treated as light sources（已经被照亮的面也可以被认为是光源，生成 VPL 之后，使用直接光照就行）
- Approach
  - Shoot light sub-paths and assume the end point of each sub-path is a Virtual Point Light (VPL) 
  - Render the scene as usual using these VPLs

![image-20221121161511303](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211615339.png)

- Pros: fast and usually gives good results on diffuse scenes
- Cons
  - Spikes will emerge when VPLs are close to shading points （在窄的缝隙和接缝出有问题）
  - Cannot handle glossy materials

## Advanced Appearance Modeling

- Non-surface models 
  - Participating media 
  - Hair / fur / fiber (BCSDF) 
  - Granular material 

- Surface models
  - Translucent material (BSSRDF)
  - Cloth
  - Detailed material (non-statistical BRDF) 
- Procedural appearance

### Non-Surface Models

#### Participating Media

- Participating Media（散射介质）: Fog, Cloud, Hair(考虑光线和一根曲线的作用)
  - 不在表面上而是在空间中
- At any point as light travels through a participating medium, it can be **(partially) absorbed** and **scattered**.

![image-20221121162149763](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211621790.png)

- Use **Phase Function** to describe the angular distribution of light scattering at any point x within participating media
  - 决定光线如何散射

![image-20221121162320284](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211623310.png)

#### Participating Media: Rendering

- Randomly choose a direction to bounce
- Randomly choose a distance to go straight
- At each ‘shading point’, connect to the light

![image-20221121162850934](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211628974.png)

#### Hair Appearance

##### Kajiya-Kay Model

- 只考虑反射

![image-20221121162959158](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211629187.png)

![image-20221121163011905](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211630986.png)

##### Marschner Model

- 考虑三种光线与头发圆柱的作用
  - R: 光线被头发表面反射
  - TT: 光线进入头发从头发另一侧折射出
  - TRT: 光线从头发底面被反射，从入射一侧折射出

![image-20221121163030225](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211630253.png)

![image-20221121163112524](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211631558.png)

![image-20221121163309432](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211633536.png)

#### Fur Appearance — As Human Hair

- Cannot represent diffusive and saturated appearance

![image-20221121163555677](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211635751.png)

![image-20221121163619256](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211636309.png)

- 动物的 medulla size 大

##### Double Cylinder Model

![image-20221121163817447](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211638476.png)

![image-20221121163828936](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211638967.png)

![image-20221121163842943](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211638028.png)

#### Granular Material

- 颗粒材质

![image-20221121164318568](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211643639.png)

![image-20221121164443755](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211644845.png)

### Surface Models

#### Translucent Material

- translucent: 光线可以从一个地方进入物体，从另外一个面钻出
- like: Jade, Jellyfish

#### Subsurface Scattering

- Visual characteristics of many surfaces caused by light exiting at different points than it enters 
- 对 BRDF 的延申：从一个点进来，从另外一个其他点出去

#### Scattering Functions

- BSSRDF: generalization of BRDF; exitant radiance at one point due to incident differential irradiance at another point:


$$
S\left(x_i, \omega_i, x_o, \omega_o\right)
$$


- Generalization of rendering equation: integrating over all points on the surface and all directions (!)


$$
L\left(x_o, \omega_o\right)=\int_A \int_{H^2} S\left(x_i, \omega_i, x_o, \omega_o\right) L_i\left(x_i, \omega_i\right) \cos \theta_i \mathrm{~d} \omega_i \mathrm{~d} A
$$



![image-20221121164857212](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211648242.png)

- Approximate light diffusion by introducing two point sources.

![image-20221121164949456](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211649493.png)

- Example

![image-20221121165042805](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211650855.png)

### Cloth

- A collection of twisted fibers!
- Two levels of twist

![image-20221121165406390](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211654419.png)

- Woven or knitted 

![image-20221121165424080](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211654140.png)

- Render as Surface
  - Given the weaving pattern, calculate the overall behavior
  - Render using a BRDF 

![image-20221121165721165](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211657282.png)

- Render as Participating Media
  - Properties of individual fibers & their distribution $\to$ scattering parameters 
  - Render as a participating medium

![image-20221121165705878](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211657900.png)

- Render as Actual Fibers
  - Render every fiber explicitly! 

![image-20221121165825429](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211658650.png)

### Detailed Appearance: Motivation

- 真实世界中的物体是有瑕疵的，描述方法得到的方法过于完美，所以显得不真实
- 可以在物体渲染时手动加入瑕疵

![image-20221121170312582](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211703658.png)

![image-20221121170325002](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211703081.png)

![image-20221121170335863](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211703935.png)

### Recap: Microfacet BRDF

![image-20221121170532505](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211705542.png)

![image-20221121170542012](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211705049.png)

#### Difficult path sampling problem

- 微表面反射的光线反射不到摄像机上

![image-20221121170713789](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211707841.png)

#### Solution: BRDF over a pixel

![image-20221121170737705](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211707743.png)

### Recent Trend: Wave Optics

![image-20221121171220925](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2022/202211211712003.png)

## Procedural Appearance

- 定义三维的纹理：$f(x,y,z)$ 查询得到纹理
- define details without textures
  - Compute a noise function on the fly
  - 3D noise $\to$ internal structure if cut or broken