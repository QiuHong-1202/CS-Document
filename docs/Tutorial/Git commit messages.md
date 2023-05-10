# Git commit messages

## Commit messages 的格式

```
<type>(<scope>): <subject>
```

### type(必须)

- feat：新功能（feature）
- fix/to：修复bug
  - fix：产生diff并自动修复此问题。适合于一次提交直接修复问题
  - to：只产生diff不自动修复此问题。适合于多次提交。最终修复问题提交时使用fix
- docs：文档（documentation）
- style：格式（不影响代码运行的变动），仅仅修改了空格、格式缩进等等
- refactor：重构（即不是新增功能，也不是修改bug的代码变动）
- perf：优化相关，比如提升性能、体验。
- test：增加测试
- chore：改变构建流程、或者增加依赖库、工具等
- revert：回滚到上一个版本
- merge：代码合并
- sync：同步主线或分支的Bug

### scope(可选)

scope用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

如果修改影响了不止一个scope，可以使用 `*` 代替。

### subject(必须)

commit目的的简短描述，不超过50个字符

## 参考

- [如何写好 Git commit messages](https://www.cnblogs.com/cpselvis/p/6423874.html)