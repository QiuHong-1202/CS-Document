# vcpkg

## Notice

- 在运行旧版本代码时，尽量不使用 vcpkg，因为 vcpkg 只会安装最新版本的包，想要安装自己想要的版本，最好的方式就是自己编译
- 自行编译的步骤：
    - 在 cmake 中 cofigure 和 generate 后 `build` 项目
    - build `install`  （注意修改 cmake 中的 `install-prefix` 为自己想要的路径）

- [Visual Studio版本号、MSVC版本、工具集版本号](https://blog.csdn.net/sanqima/article/details/117849324)

## Install

前置条件：

- Windows 7 or newer
- [Git](https://git-scm.com/downloads)
- [Visual Studio](https://visualstudio.microsoft.com/) 2015 Update 3 or greater with the **English language pack**

执行如下命令：

- 下载 vcpkg，此操作会创建一个名为 `vcpkg` 的目录

```
git clone https://github.com/microsoft/vcpkg
```

- 执行 `bootstrap-vcpkg.bat` 文件，就安装完成

```
.\vcpkg\bootstrap-vcpkg.bat
```

## Package Install

转到 vcpkg 的安装目录下

- 默认安装 `x86` 的包，要使用 `x64`，需要添加 `:x64-windows`

```
vcpkg.exe install [packages to install]
```

```
vcpkg.exe install [package name]:x64-windows
```

```
vcpkg.exe install [packages to install] --triplet=x64-windows
```

- 搜索包
    - 官网搜索：https://vcpkg.io/en/packages.html

```
vcpkg.exe search [search term]
```

## Integrate

- 将 vcpkg 和 Visual Studio 集成

```
vcpkg.exe integrate install
```

- 移除集成（**卸载 vcpkg 前必须要移除**）

```
vcpkg integrate remove
```

## More Commands

- https://blog.csdn.net/hfy1237/article/details/129879378

## Folder Explanations

- buildtrees - 包含从中生成每个库的源的子文件夹，一般在xxxx.clean文件夹下。
- docs - 文档和示例。
- downloads - 所有已下载的工具或源的缓存副本。 运行安装命令时，vcpkg 会首先搜索此处。
- installed - 包含每个已安装库的标头和二进制文件。 与 Visual Studio 集成时，实质上是相当于告知它将此文件夹添加到其搜索路径。
- packages - 在不同的安装之间用于暂存的内部文件夹。
- ports - 用于描述每个库的目录、版本和下载位置的文件。 如有需要，可添加自己的端口。
- scripts - 由 vcpkg 使用的脚本（CMake、PowerShell）。
- toolsrc - vcpkg 和相关组件的 C++ 源代码。
- triplets - 包含每个受支持目标平台（如 x86-windows 或 x64-uwp）的设置。

