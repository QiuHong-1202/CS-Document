## Layout Article 

- `[ICCV19]` **LayoutVAE**: Stochastic Scene Layout Generation From a Label Set
  - model: VAE
  - task: 根据 label set, per label layouts in existing image 进行有条件生成

- `[CVPR21]` **LayoutTransformer**: Layout generation and completion with self attention
  - model: transformer
  - task: completion
- `[MM21]` **LayoutGAN++**: Constrained Graphic Layout Generation via Latent Optimization
  - model: GAN
- `[ECCV22]` **BLT**: Bidirectional layout transformer for controllable layout generation
  - model: transformer & BERT
  - task: 根据 element, category 进行有条件生成，无条件生成
  - pros:
    - hierarchical mask sampling policy，一个改进了的 mask 方法，而不是直接应用 Transformer 的 mask
  - cons: 
    - 不能处理元素之间的关系

- `[CVPR23]` **LayoutFormer++**: Conditional Graphic Layout Generation via Constraint Serialization and Decoding Space Restriction
  - model: transformer
  - condition: 根据 type, relationship, type & size 进行有条件生成, refinement, completion, 无条件生成
  - pros: 
    - 灵活性和可控性强
    - A constraint serialization scheme which can handle diverse constrain
    - A sequence to sequence layout generation method

- `[CVPR23]` **LayoutDM**: Discrete Diffusion Model for Controllable Layout Generation
  - model: diffusion
  - task: Category $\to$ Size+Position, Category+Size $\to$ Position, Completion, 无条件生成
  - pro:
    - padding approach to model highly structured layout data
    - masking and logit adjustment during the inference
  - cons:
    - 作者在进行训练和评估模型时，剔除了数据集中元素个数 $\ge50$ 的 layout 数据，在输入文档具有更多元素时，模型的性能会降低
- `[CVPR23]` **LDGM**: Unifying Layout Generation with a Decoupled Diffusion Model
  - model: diffusion
  - task: 根据 $(c,x,y,w,h)$ 五种属性进行有条件生成, refinement, completion, 无条件生成
  - pros: 
    - 对于类别属性 $(c)$、位置属性 $(x, y)$ 和大小属性 $(w, h)$ 构造了三条 timeline 分别添加噪声

