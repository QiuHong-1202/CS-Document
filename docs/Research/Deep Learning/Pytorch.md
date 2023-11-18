# Pytorch

## Problems

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

### self.data & data

在 Python 类中，`self.data` 和 `data` 这两个变量在使用上有一些区别：

1. `self.data`：这是类的实例变量，通常用于在类的方法中引用类实例的属性。在类中定义的变量，如果带有 `self` 前缀，表示它是该类的实例属性。这意味着每个类的实例都会有自己的 `self.data` 属性，它们相互之间独立。当在类的方法中需要引用实例属性时，应该使用 `self.data`。

2. `data`：这是一个普通的局部变量或者是方法的参数。在类的方法中，如果没有带有 `self` 前缀的变量，它就是一个局部变量或者是方法的参数。这些变量的作用范围仅限于所在的方法，不影响其他方法和类的实例。

下面是一个示例，用于演示这两者之间的区别：

```python
class MyClass:
    def __init__(self, data):
        self.data = data  # 类的实例变量 self.data

    def print_data(self, data):
        # data 是方法的参数
        print("Instance data (self.data):", self.data)
        print("Method parameter (data):", data)

# 创建类实例
obj = MyClass("Instance variable value")

# 调用类的方法，并传递一个参数
obj.print_data("Method parameter value")
```

在上述示例中，`self.data` 是类 `MyClass` 的实例变量，表示每个类的实例都有一个独立的 `self.data` 属性。而在 `print_data` 方法中的 `data` 是该方法的参数，它只在方法执行期间有意义，不影响类的实例。

输出结果：
```
Instance data (self.data): Instance variable value
Method parameter (data): Method parameter value
```

总结：`self.data` 是类的实例变量，每个类的实例都有一个独立的属性。而 `data` 是方法的参数或者局部变量，仅在方法的作用域内有效。

### 防止 pytroch 并行化下对模型的封装不能获得原始模型

```py
raw_model = model.module if hasattr(self.model, "module") else model
```

这句代码的意思是将`model`赋值给`raw_model`，但它根据条件进行了一些处理。让我们来解释这个条件语句：

- `hasattr(self.model, "module")` 检查 `self.model` 是否具有名为 "module" 的属性。
- 如果 `self.model` 具有 "module" 属性，那么 `raw_model` 将被赋值为 `self.model.module`。
- 否则，`raw_model` 将被赋值为 `model` 本身。

这个条件语句的目的是处理模型并行化的情况。在某些情况下，模型会被封装在 `torch.nn.DataParallel` 中，这会导致 `model` 本身被包装在一个额外的层级中。所以，为了确保在后续的代码中使用正确的模型，需要对这种情况进行处理。

如果 `self.model` 具有 "module" 属性，那么它意味着模型被封装在 `torch.nn.DataParallel` 中，因此需要通过 `self.model.module` 来访问原始的模型。

如果 `self.model` 没有 "module" 属性，那么它意味着模型没有被封装在 `torch.nn.DataParallel` 中，所以可以直接使用 `model`。

通过这种方式，无论模型是否被并行化，都能确保获得正确的原始模型，并将其赋值给`raw_model` 变量。

### 输出整个 tensor

```py
torch.set_printoptions(profile="full")
print(x) # prints the whole tensor
torch.set_printoptions(profile="default") # reset
print(x) # prints the truncated tensor
```

### 训练时 loss 尖峰

保持总数据量能够整除 batch_size 可以避免这一情况，在 batch 较小时，随机性增大，导致 loss 增大

## Links

- 为什么 Cross Entropy 的计算结果不为 0：[Cross Entropy in PyTorch](https://stackoverflow.com/questions/49390842/cross-entropy-in-pytorch)
