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





