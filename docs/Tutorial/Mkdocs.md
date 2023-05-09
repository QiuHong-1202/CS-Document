# Mkdocs

## Useful Links

- [Mkdocs Official Document](https://www.mkdocs.org/getting-started/)
- [Mkdocs-material Document](https://squidfunk.github.io/mkdocs-material/)

## 安装 Mkdocs

> 在 conda 虚拟环境中安装

- 安装 `pip`

```
conda install pip
```

- 安装 `mkdocs`

```
pip install mkdocs
```

- [Install Guide](https://www.mkdocs.org/user-guide/installation/)

## 安装 material 主题

```
pip install mkdocs-material
```

## 常用命令

- 在 mkdocs 命令前要加入 `python -m`

### 创建项目

```
mkdocs new my-project
cd my-project
```

### 测试项目

```
mkdocs serve
```

## 部署文档

- 目录结构

```
CS-Doucment/
    mkdocs.yml
    docs/
qiuhong-1202.github.io/
```

- 转到 Pages 仓库目录下

```
cd ../qiuhong-1202.github.io/
```

- 部署到 Github Pages

```
python -m mkdocs gh-deploy --config-file ../CS-Document/mkdocs.yml --remote-branch main
```

