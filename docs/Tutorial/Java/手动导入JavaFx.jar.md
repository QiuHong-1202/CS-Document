## 手动导入JavaFx.jar

- JavaFX Scene Builder：[JavaFX Scene Builder 1.x Archive (oracle.com)](https://www.oracle.com/java/technologies/javafxscenebuilder-1x-archive-downloads.html)

- JavaFX SDK download：[JavaFX - Gluon (gluonhq.com)](https://gluonhq.com/products/javafx/)

1. 进入官网下载 `JavaFX JAR`
2. 在 Libraries 中添加 `lib` 路径

```
File->Project Structure->Project Settings->Libraries
```

`lib` 的路径指向的是刚才解压的 JavaFX 压缩包的 `lib` 路径

![添加lib路径](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210704002411.png)

3. 添加`Path`变量

```
File->Settings->Appearance & Behavior ->Path Variables
```

变量名为`PATH_TO_FX`，路径为之前的 `lib` 路径

![添加Path变量](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210704002539.png)

4. 编辑配置

```
--module-path ${PATH_TO_FX} --add-modules javafx.controls,javafx.fxml
```

- 找到 `Edit Configurations`，填入上述代码到 `VM options`

![image-20210704002632845](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210704002632.png)

![image-20210704002647950](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210704002647.png)

![image-20210704002659552](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210704002659.png)

