---
title: create-react-app中使用typescript
date: 2020-04-25 14:46:56
tags: [react, typescript]
---

记录下在create-react-app中使用typescript的过程
<!-- more -->

## 环境和安装

1. 安装create-react-app

    `npm install -g create-react-app`

2. 使用create-react-app构建项目

    `npx create-react-app 项目名称 --typescript`

    加上 `--typescript` 是通过ts来构建项目

3. 已有的 `create-react-app` 项目可通过

    ```cmd
    npm install --save typescript @types/node @types/react @types/react-dom @types/jest

    # 或者

    yarn add typescript @types/node @types/react @types/react-dom @types/jest
    ```

    添加typescript

## 在typescript中引入react-router-dom

需要安装2个依赖包

`yarn add --dev react-router-dom @types/react-router-dom`

`react-router-dom` 这个包是react-router的核心包

`@types/react-router-dom` 这个包是typescript的声明文件

之后就可以在项目中使用

```typescript
import {
  BrowserRouter as Router,
  Route,
  Switch,
  Redirect
} from 'react-router-dom'
```

## 第三方包的引入

大多数的第三方包没有Ts类型文件

在编辑器中会报警告

`无法找到模块“xxx”的声明文件`

这里我们需要在xx.d.ts文件中声明

```typescript
declare module 'xx' {
  const moduleName: any
  export default moduleName
}
```

声明他其中的类型都为 `any` 或者 模块的应该有的类型
