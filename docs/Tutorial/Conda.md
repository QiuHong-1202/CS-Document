# Conda

## 安装和镜像配置

### 地址

- [Anaconda 镜像](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)
- [Anaconda 下载](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/)
- [MiniConda 下载](https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/)

### 注意事项

- 尽量选择 MiniCoda
- 安装时尽量安装到 `User` 目录 (无需管理员权限)

### Pytorch v1.8.2 with LTS support (Python <= 3.8)

```
# CUDA 10.2
# NOTE: PyTorch LTS version 1.8.2 is only supported for Python <= 3.8.
conda install pytorch torchvision torchaudio cudatoolkit=10.2 -c pytorch-lts

# CUDA 11.1 (Linux)
# NOTE: 'nvidia' channel is required for cudatoolkit 11.1 <br> <b>NOTE:</b> Pytorch LTS version 1.8.2 is only supported for Python <= 3.8.
conda install pytorch torchvision torchaudio cudatoolkit=11.1 -c pytorch-lts -c nvidia

# CUDA 11.1 (Windows)
# 'conda-forge' channel is required for cudatoolkit 11.1 <br> <b>NOTE:</b> Pytorch LTS version 1.8.2 is only supported for Python <= 3.8.
conda install pytorch torchvision torchaudio cudatoolkit=11.1 -c pytorch-lts -c conda-forge

# CPU Only
# Pytorch LTS version 1.8.2 is only supported for Python <= 3.8.
conda install pytorch torchvision torchaudio cpuonly -c pytorch-lts

# ROCM5.x

Not supported in LTS.



# CUDA 10.2
pip3 install torch==1.8.2 torchvision==0.9.2 torchaudio==0.8.2 --extra-index-url https://download.pytorch.org/whl/lts/1.8/cu102

# CUDA 11.1
pip3 install torch==1.8.2 torchvision==0.9.2 torchaudio==0.8.2 --extra-index-url https://download.pytorch.org/whl/lts/1.8/cu111

# CPU Only
pip3 install torch==1.8.2 torchvision==0.9.2 torchaudio==0.8.2 --extra-index-url https://download.pytorch.org/whl/lts/1.8/cpu

# ROCM5.x

Not supported in LTS.
```

## Commands

### 缓存清理

- Conda

```
# 删除没有用的包
conda clean -p
# 删除tar打包
conda clean -t
# 删除无用的包和缓存
conda clean --all
```

- PIP (Linux)

```
rm -rf ~/.cache/pip
```

- PIP (Windows)

```
# 删除下面的文件夹
C:\Users\username\AppData\Local\pip\cache
```

### Conda 自身

- 查看当前 conda工具版本号

```bash
conda --version
```

- 查看包括版本的更多信息

```bash
conda info
```

- 更新 conda 至最新版本（为所有用户安装的版本需要管理员权限）

```bash
conda update -n base -c defaults conda
```

- 查看 conda 帮助信息

```bash
conda -h
```

### 环境管理

- 查看 conda 环境管理命令帮助信息

```bash
conda create --help
```

- 创建出来的虚拟环境所在的位置为 conda 路径下的 `env/` 文件下，默认创建和当前 python 版本一致的环境

```bash
conda create --name envname
```

- 创建新环境时指定 python 版本为 3.6，环境名称为 python36

```bash
conda create --name python36 python=3.6
```

- 切换到环境名为 python36 的环境（默认是 base 环境），切换后可通过 `python -V` 查看是否切换成功

```bash
conda activate python36
```

- 返回前一个 python 环境

```bash
conda deactivate
```

- 显示已创建的环境，会列出所有的环境名和对应路径

```bash
conda info -e
```

- 删除虚拟环境

```bash
conda remove --name envname --all
```

- 指定 python 版本,以及多个包

```bash
conda create -n envname python=3.4 scipy=0.15.0 astroib numpy
```

- 查看当前环境安装的包

```bash
conda list   ##获取当前环境中已安装的包
conda list -n python36   ##获取指定环境中已安装的包
```

- 克隆一个环境

```bash
# clone_env 代指克隆得到的新环境的名称
# envname 代指被克隆的环境的名称
conda create --name clone_env --clone envname

#查看conda环境信息
conda info --envs
```

- 构建相同的conda环境(不通过克隆的方法)

```bash
# 查看包信息
conda list --explicit

# 导出包信息到当前目录, spec-file.txt为导出文件名称,可以自行修改名称
conda list --explicit > spec-file.txt

# 使用包信息文件建立和之前相同的环境
conda create --name newenv --file spec-file.txt

# 使用包信息文件向一个已经存在的环境中安装指定包
conda install --name newenv --file spec-file.txt
```

- 查找包

```bash
# 模糊查找，即模糊匹配，只要含py字符串的包名就能匹配到
conda search py   

# 查找包，--full-name表示精确查找，即完全匹配名为python的包
conda search --full-name python
```

- 安装更新删除包

```bash
# 在当前环境中安装包
conda install scrapy  

# 在指定环境中安装包
conda install -n python36 scrapy

# 在当前环境中更新包  
conda update scrapy   

# 在指定环境中更新包
conda update -n python36 scrapy  

# 更新当前环境所有包
conda update --all   

# 在当前环境中删除包
conda remove scrapy   

# 在指定环境中删除包
conda remove -n python2 scrapy
```

### Python 管理

- 查找可以安装的 python

```bash
# 查找所有名称包含 python 的包
conda search python

# 查找全名为 python 的包
conda search --full-name python
```

- 安装不同版本的 python

```bash
# 在不影响当前版本的情况下,新建环境并安装不同版本的python
# 新建一个 Python 版本为 3.6 名称为 py36 的环境
conda create -n py36 python=3.6 anaconda

# 注:将py36替换为您要创建的环境的名称。anaconda是元数据包，带这个会把base的基础包一起安装，不带的话新环境只包含python3.6相关的包。 python = 3.6是您要在此新环境中安装的软件包和版本。 这可以是任何包，例如numpy = 1.7，或多个包。
# 然后激活想要使用的环境即可
conda activate py36

# 更新Python
# 普通的更新python
conda update python

# 将python更新到另外一个版本/安装指定版本的python
conda install python=3.6
```

### 分享环境

如果你想把你当前的环境配置与别人分享，这样他人可以快速建立一个与你一模一样的环境（同一个版本的 python 及各种包）来共同开发/进行新的实验。一个分享环境的快速方法就是给他人一个你的环境的 `.yml` 文件

- 首先通过 `activate target_env` 要分享的环境 `target_env`，然后输入下面的命令会在当前工作目录下生成一个 `environment.yml` 文件

```bash
conda env export > environment.yml
```

- 小伙伴拿到 `environment.yml` 文件后，将该文件放在工作目录下，可以通过以下命令从该文件创建环境

```bash
conda env create -f environment.yml
```