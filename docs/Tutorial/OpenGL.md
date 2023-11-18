# OpenGL



## glUniformMatrix4fv

`glUniformMatrix4fv` 是 OpenGL 中的一个函数，用于将值传递给着色器中的 uniform 变量。该函数的原型如下：

```c
void glUniformMatrix4fv(GLint location, GLsizei count, GLboolean transpose, const GLfloat *value);
```

- `location`：指定要修改的 uniform 变量的位置。
- `count`：指定要修改的矩阵数量。
- `transpose`：指示是否需要转置矩阵。
- `value`：指向一个或多个矩阵的指针。

在这个函数中，`GL_FALSE` 和 `GL_TRUE` 是 `GLboolean` 类型的值，它们用来指示传递给着色器的矩阵是否需要在上传之前被转置（即交换行和列）。

- `GL_FALSE`：表示不需要转置矩阵。这是最常用的选项，因为 OpenGL 期望矩阵以列主序（column-major order）存储，而大多数 C/C++ 代码中的矩阵都是按列主序存储的。
- `GL_TRUE`：表示需要在传递给着色器之前转置矩阵。如果你的矩阵是以行主序（row-major order）存储的，可以使用这个选项。

