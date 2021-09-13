# 提交限制

- husky 在 `git` 中创建钩子
- lint-staged 对暂存区进行操作

```shell
npm install -D husky lint-staged
```

**_需要在 `package.json` 中添加两条 `script`_**

- prepare 会在执行 `npm install` 后执行
- lint 协助 `husky` 执行 `lint-staged`

```json
{
    ...
    "script": {
        "prepare": "husky install",
        "lint": "lint-staged"
    }
}
```

**_在执行完 `husky install` 后为 `git` 添加钩子_**

- 添加 `commit` 操作钩子

_执行下列语句后会自动创建 `.husky/pre-commit` 脚本文件_

```shell
npx husky add .husky/pre-commit
```

- 添加 `commit` 信息校验钩子

_执行下列语句后会自动创建 `.husky/commit-msg` 脚本文件_

```shell
npx husky add .husky/commit-msg
```

**_在 `package.json` 中添加 `lint-staged` 对象_**

使用 `eslint` 对 `src` 目录下进行检查，并修复部分项；将自动修复的文件添加到 `git` 暂存区。

```json
{
    ...
    "lint-staged": {
        "src/**/*": [
            "eslint --fix --max-warnings 0",
            "git add"
        ]
    }
}
```
