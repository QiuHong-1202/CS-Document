# Windows Debug

## 下载文件夹变为 download

- 新建一个记事本，打开记事本，将下面代码复制进去

```
[.ShellClassInfo]
LocalizedResourceName=@%SystemRoot%system32shell32.dll,-21798
IconResource=%SystemRoot%system32imageres.dll,-184
```

- 点击【文件】-【另存为】，将保存路径设置为： `C:\Users\hongliang\Downloads` ，然后将保存类型改成【所有文件】，将文件名修改为：`desktop.ini`  点击保存（此时可能会弹出是否覆盖，点击 “是” ）

- 使用管理员命令行输入以下内容

```
attrib +R C:\Users\hongliang\Downloads
attrib +S +H C:\Users\hongliang\Downloads\desktop.ini
```

