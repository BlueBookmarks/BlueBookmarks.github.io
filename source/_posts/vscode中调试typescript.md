---
title: vscode中调试typescript
date: 2019-12-25 15:38:31
tags: [vscode, typescript]
---

vscode中调试typescript
<!-- more -->

## 目录

- [依赖包](#依赖包)
- [配置tsconfig.json](#配置tsconfigjson)
- [配置launch.json](#配置launchjson)
- [开始调试](#开始调试)

## 依赖包

```node
// npm安装
npm i typescript
npm i ts-node
// yarn安装
yarn add typescript
yarn add ts-node
```

## 配置tsconfig.json

- 初始化tsconfig.json

  `tsc --init`

- 配置tsconfig.json

  ```json
    {
      "compilerOptions": {
        "module": "commonjs",
        "target": "es5",
        "noImplicitAny": true,
        "outDir": "./dist",
        "sourceMap": true
      },
      "include": [
        "src/**/*"
      ]
    }
  ```

## 配置launch.json

- 打开调试 `alt + D`

- 选择添加配置

- 编辑launch.json

  ```json
  {
    "version": "0.2.0",
    "configurations": [
      {
        "name": "Current TS File",
        "type": "node",
        "request": "launch",
        "program": "${workspaceRoot}/node_modules/ts-node/dist/bin.js",
        "args": [
            "${relativeFile}"
        ],
        "cwd": "${workspaceRoot}",
        "protocol": "inspector"
      }
    ]
  }
  ```

## 开始调试

- 打开对应的ts文件

- 打开调试 `alt + D`

- 选择启动调试
