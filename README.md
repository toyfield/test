## README

这是一个 github 仓库，用来测试发布github npm package

## 发布步骤

根据 [npm registry 文档](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-npm-registry) 进行操作。

### 1. 配置权限

1. 配置 personal access token，允许 package:write 权限。
2. 配置 ~/.npmrc 配置

```shell
# TOKEN 为第一步中拿到的 personal access token
//npm.pkg.github.com/:_authToken=TOKEN
```

### 2. npm 发布配置

有两种方式：

1. 在项目根目录，创建 `.npmrc` 文件，填写以下内容即可：  
```
@NAMESPACE:registry=https://npm.pkg.github.com
```
其中 `NAMESPACE` 是 github org 或者 account 的名称。
2. 在 package.json 中，填写以下字段：  
```json
"publishConfig": {
    "registry": "https://npm.pkg.github.com"
}
```

推荐第一种，因为拉取 package 时，仍然需要以上配置。

### 3. 确认 package.json 配置

3. 确认 package.json 中的名字，包含 scope 部分，为第二步的 `NAMESPACE`。
4. 确认 package.json 中的 repository 字段，是对应的 github 仓库地址。

### 4. 发布 package

```shell
# 根据自己的管理软件进行 publish，publish 前一般要 build
pnpm publish
```

### monorepo

根据[文档](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-npm-registry#authenticating-to-github-packages) 只需要每个 package.json 的 repository 字段都指向 github 仓库地址即可。

## 使用

安装包也只需要给根目录或者全局的 .npmrc 文件配置以下内容即可：

```
@NAMESPACE:registry=https://npm.pkg.github.com
```

## 权限

仓库默认是 private 的，所以只有有权限的人才能拉取包。但是很神奇的是默认不允许组织内的人可以拉取，那个权限是 internal。
同时，需要先在 org 中的 setting - packages 设置可以调整的权限，默认只有 private，需要手动开放 internal 和 public，然后 org - packages 中才能调整各个 package 的权限。

另外，虽然在 package.json 中写了 repository 字段，但是在 github 上并不会直接 link，需要在 package 中自行 link，可以参考[文档](https://docs.github.com/en/packages/learn-github-packages/connecting-a-repository-to-a-package)

link 后，package 的读写权限，会自动继承自 link 的 repo。

>注意，不管 package 是否为 public，都需要配置 .npmrc 的 github personal access token，否则无法拉取。