# Getting Start 

## Dataset provided by pytorch

PyTorch offers domain-specific libraries such as TorchText, TorchVision, and TorchAudio, all of which include datasets. For this tutorial, we will be using a TorchVision dataset.

The `torchvision.datasets` module contains Dataset objects for many real-world vision data like CIFAR, COCO ([full list here](https://pytorch.org/vision/stable/datasets.html)). In this tutorial, we use the FashionMNIST dataset. Every TorchVision Dataset includes two arguments: `transform` and `target_transform` to modify the samples and labels respectively.

```python
from torchvision import datasets
from torchvision.transforms import ToTensor

# Download training data from open datasets.
training_data = datasets.FashionMNIST(
    root="data",
    train=True,
    download=True,
    transform=ToTensor(),
)

# Download test data from open datasets.
test_data = datasets.FashionMNIST(
    root="data",
    train=False,
    download=True,
    transform=ToTensor(),
)
```

## Tensor

Pytorch 的一大作用就是可以代替 Numpy 库，所以首先介绍 Tensors ，也就是张量，它相当于 Numpy 的多维数组(ndarrays)。两者的区别就是 Tensors 可以应用到 GPU 上加快计算速度。

## Autograd

对于 Pytorch 的神经网络来说，非常关键的一个库就是 `autograd` ，它主要是提供了对 Tensors 上所有运算操作的自动微分功能，也就是计算梯度的功能。它属于 `define-by-run` 类型框架，即反向传播操作的定义是根据代码的运行方式，因此每次迭代都可以是不同的。



