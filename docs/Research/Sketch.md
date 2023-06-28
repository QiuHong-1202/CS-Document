## Sketch Article

- `[ICLR18]` **SketchRNN**: A neural representation of sketch drawings
  - 功能：无条件生成、条件重建、插值、不改变原有笔画地进行预测（给定的笔画较少、生成概念性的草图、要求在现有输入笔画的上方顺序排列）
  - 架构：bidirectional RNN(LSTM) encoder，HyperLSTM decoder
- `[CVPR20]` **Sketchformer**: Transformer-based Representation for Sketched Structure
  - 功能：sketch 的分类、 sketch 重建、sketch based Image retrieval、sketch 的插值
  - 架构：Transformer encoder & decoder
  - 为什么不使用 LSTM 而使用 Transformer 作为 decoder：作者认为 seq2seq 模型的有限时间范围可能会阻止这种表示法对长而复杂的草图进行建模

- `[BMVC20]` **SketchHealer**: A Graph-to-Sequence Network for Recreating Partial Human Sketches
  - 功能：sketch healing
  - 架构：GCN-based encoder，LSTM decoder
  
- `[ICCV21]` **SketchLattice**: Latticed Representation for Sketch Manipulation
  - 功能：sketch healing、基于图像的草图合成
  - 架构：利用一个网格图 (Lattice Graph) 对草图图像进行采样以生成草图的网格表示，GCN-based encoder，LSTM decoder

- `[IJCV22]` **SketchHealer-2.0**: Generative Sketch Healing
  - 功能：sketch healing（对于随机缺失的笔画 $p_{mask}$ 进行重绘，作者特意强调了自己的任务是修复并且和 SketchRNN 不改变原有笔画的预测任务 `completion` 不同）
  - 架构：GCN encoder，LSTM decoder
  - 和 `SketchHealer1.0` 相比，增加了一个 `Perceptual Metric` 

- `[AAAI23]` **SP-gra2seq**: Linking Sketch Patches by Learning Synonymous Proximity for Graphic Sketch Representation
  - 功能：sketch healing
  - 架构：使用 CNN encoder 获取 patch，GCN encoder 进行特征提取，RNN decoder 进行重建

- `[ICLR23]` **SketchKnitter**: Vectorized Sketch Generation with Diffusion Models
  - 功能：sketch 的无条件和有条件生成
  - 架构：diffusion



## 数据集

- QuickDraw50M
  - 包含 345 个对象类别的超过 5000 万个草图, 草图包含笔画序列