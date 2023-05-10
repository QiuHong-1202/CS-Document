# Mkdocs

## Document

- [Mkdocs Official Document](https://www.mkdocs.org/getting-started/)
- [Mkdocs-material Document](https://squidfunk.github.io/mkdocs-material/)
- [Installation Guide](https://www.mkdocs.org/user-guide/installation/)

## 安装 Mkdocs

> 在 conda 虚拟环境中安装

- 创建 conda 虚拟环境

```sh
conda create --name mkdocs python=3.9
```

- 安装 `pip`

```sh
conda install pip
```

- 安装 `mkdocs`

```sh
pip install mkdocs
```

## 安装 material 主题

```sh
pip install mkdocs-material
```

## 常用命令

- 在 mkdocs 命令前要加入 `python -m`

### 创建项目

```sh
mkdocs new my-project
cd my-project
```

### 测试项目

- 切换到 Doc 目录下

```shell
cd D:/Projects/Site/CS-Document
```

- 启动测试服务

```sh
python -m mkdocs serve
```

## 部署文档

- 目录结构

```
CS-Doucment/
    mkdocs.yml
    docs/
qiuhong-1202.github.io/
```

- 激活 `mkdocs` 虚拟环境

```shell
conda activate mkdocs
```

- 转到 Doc 目录编写文档

```shell
cd D:/Projects/Site/CS-Document
```

- 转到 Pages 仓库目录下

```sh
cd ../qiuhong-1202.github.io/
```

- 部署到 Github Pages

```sh
python -m mkdocs gh-deploy --config-file ../CS-Document/mkdocs.yml --remote-branch main
```

## 参考

- [TonyCrane's Notebook Repo](https://github.com/TonyCrane/note)
- [TonyCrane's Notebook](https://note.tonycrane.cc/)
