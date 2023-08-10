# Proxy

## 设置终端的临时代理

- 在终端关闭后代理就会失效


```
set HTTP_PROXY=http://127.0.0.1:7890
```

```
set HTTPS_PROXY=http://127.0.0.1:7890
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

