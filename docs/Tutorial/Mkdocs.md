# Mkdocs

## Document

- [Mkdocs Official Document](https://www.mkdocs.org/getting-started/)
- [Mkdocs-material Document](https://squidfunk.github.io/mkdocs-material/)
- [Installation Guide](https://www.mkdocs.org/user-guide/installation/)

## 安装 Mkdocs

> 在 conda 虚拟环境中安装

- 创建 conda 虚拟环境

```bash
conda create --name mkdocs python=3.9
```

- 安装 `pip`

```bash
conda install pip
```

- 安装 `mkdocs`

```bash
pip install mkdocs
```

## 安装 material 主题

```bash
pip install mkdocs-material
```

## 常用命令

- 在 mkdocs 命令前要加入 `python -m`

### 创建项目

```bash
mkdocs new my-project
cd my-project
```

### 测试项目

- 切换到 Doc 目录下

```bash
cd D:/Projects/Site/CS-Document
```

- 启动测试服务

```bash
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

```bash
conda activate mkdocs
```

- 转到 Doc 目录编写文档

```bash
cd D:/Projects/Site/CS-Document
```

- 转到 Pages 仓库目录下

```bash
cd ../qiuhong-1202.github.io/
```

- 部署到 Github Pages

```bash
python -m mkdocs gh-deploy --config-file ../CS-Document/mkdocs.yml --remote-branch main
```

## Debug

- `"git-revision-date-localized"` plugin is not installed
  - 安装下列包:  `pip install mkdocs-git-revision-date-localized-plugin`

- LaTeX 无法换行：这是 MathJax 的 bug，现有的解决方法是在公式块中使用 `\displaylines{}`

- 无序标题不支持多层嵌套：需要安装额外插件并启用

  - `pip install mdx_truly_sane_lists`
  
  - 在 `mkdoc.yml` 的 `markdown_extensions` 添加 `mdx_truly_sane_lists` 



## 参考

- [TonyCrane's Notebook Repo](https://github.com/TonyCrane/note)
- [TonyCrane's Notebook](https://note.tonycrane.cc/)
