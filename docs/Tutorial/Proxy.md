# Proxy

## 设置终端的临时代理

- 在终端关闭后代理就会失效


```
set HTTP_PROXY=http://127.0.0.1:7890 
```

```
set HTTPS_PROXY=http://127.0.0.1:7890
```

- Windows

```
set HTTP_PROXY=http://127.0.0.1:7890 && set HTTPS_PROXY=http://127.0.0.1:7890
```

> Windows 一次执行多个命令 （“执行成功”的意思是返回的 `errorlevel=0`）
>
> - aa && bb：执行aa，成功后再执行bb
> - aa || bb：先执行aa，若执行成功则不再执行bb，若失败则执行bb
> - a & b：表示执行a再执行b，无论a是否成功

- Linux

```
export HTTP_PROXY=http://127.0.0.1:7890 ; export HTTPS_PROXY=http://127.0.0.1:7890
```

## 设置非系统代理应用的代理

1. 打开终端
2. 设置终端的临时代理
3. 用终端打开应用

- 例如对于 cmake-gui 使用代理，可以先设置好终端的临时代理，再执行以下命令

```
cd C:\program files\cmake\bin\
cmake-gui.exe
```

