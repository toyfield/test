## README

这是一个 github 仓库，用来测试发布github npm package

## 发布步骤

根据 [npm registry 文档](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-npm-registry) 进行操作。

1. 配置 personal access token，允许发布权限
2. 在项目根目录，创建 `.npmrc` 文件，填写`@NAMESPACE:registry=https://npm.pkg.github.com`，其中 `NAMESPACE` 是 github org 或者 account 的名称。
3. 确认 package.json 中的名字，包含 scope 部分，为第二步的 `NAMESPACE`。
4. 确认 package.json 中的 repository 字段，是对应的 github 仓库地址。
5. npm publish