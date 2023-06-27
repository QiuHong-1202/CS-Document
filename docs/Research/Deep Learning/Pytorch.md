# Pytorch

### 使用所有 CPU 核心

- 默认使用一半核心运行

```python
import os
from multiprocessing import cpu_count

cpu_num = cpu_count()  # 自动获取最大核心数目
os.environ['OMP_NUM_THREADS'] = str(cpu_num)
os.environ['OPENBLAS_NUM_THREADS'] = str(cpu_num)
os.environ['MKL_NUM_THREADS'] = str(cpu_num)
os.environ['VECLIB_MAXIMUM_THREADS'] = str(cpu_num)
os.environ['NUMEXPR_NUM_THREADS'] = str(cpu_num)
torch.set_num_threads(cpu_num)
```

### 类型标注

```python
# P.S. res: torch.Tensor 是类型标注，帮助IDE推断这是一个tensor类型
res: torch.Tensor = res[:min_len]
ans: torch.Tensor = ans[:min_len]
```

### 矩阵相关

- [torch.reshape](https://blog.csdn.net/Fluid_ray/article/details/110733893)



