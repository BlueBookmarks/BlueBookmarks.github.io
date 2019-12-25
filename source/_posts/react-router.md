---
title: react-router
date: 2019-12-25 10:43:12
tags: [react]
---

React Router 是一个基于 React 之上的强大路由库，它可以让你向应用中快速地添加视图和数据流，同时保持页面与 URL 间的同步。
<!-- more -->
## 目录

[react-router-dom](#react-router-dom)

1. [安装react-router-dom](#1-安装react-router-dom)

2. [使用react-router-dom](#2-使用react-router-dom)

3. [使用嵌套路由](#3-使用嵌套路由)

***

## react-router-dom

react-router-dom 是 react-router v4 的 web 版本

v4 和 v2, v3的区别为 v4版本把路由拆分为组件的形式可在各个模块中调用

v2/v3

```jsx
  <Router history={browserHistory}>
    <Route path="/" component={Home}>
      <IndexRoute component={HomePage} />
      <Route path="/users" component={UsersPage} />
    </Route>
  </Router>
```

v4

```JSX
  {/* App.js */}
  <BrowserRouter>
    <Home />
  </BrowserRouter>

  {/* Home.js */}
  <div>
    <div className="pages">page:
      <Route path="/" exact component={HomePage} />
      <Route path="/users" component={UsersPage} />
    </div>
  </div>
```

### 1. 安装react-router-dom

命令 `yarn add react-router-dom --dev` || `npm i react-router-dom -S`

### 2. 使用react-router-dom

```jsx
import React from 'react'
import {
  BrowserRouter as Router,
  Route,
  Link,
  Switch,
  Redirect
} from 'react-router-dom'
import Index from './pages/Index'
import Other from './pages/Other'

const App = () => (
  <Router>
    <div className="App">
      点击位置：
      <ul>
        {/* link 跳转标签 */}
        <li><Link to="/">首页</Link></li>
        <li><Link to="/other">其他</Link></li>
      </ul>
      当前页面：
      {/* Switch 只渲染一个路由 */}
      <Switch>
        {/* exact 只对当前路由匹配 */}
        <Route exact path="/" component={ Index }></Route>
        <Route path="/other" component={ Other }></Route>
        {/* 重定向  输入不存在的路径时跳转 */}
        <Redirect to="/" />
      </Switch>
    </div>
  </Router>
)

export default App

```

1. v4 版本则有了一个包含的关系：如匹配 path="/users" 的路由会匹配 path="/"的路由，在页面中这两个模块会同时进行渲染。因此，v4中多了 `exact` 关键词，表示**只对当前的路由进行匹配**

2. `<Switch>`只有一个路由会被渲染，并且**总是渲染第一个匹配到的组件**。（PS: 在第一个路由中，还是需要使用 exact，否则，当我们渲染 '/other' 或 '/other/page' 时，只会显示匹配 '/' 的组件。）

3. `<Redirect>` 组件，单独使用时，一旦当路由匹配到的时候，浏览器就会进行重定向跳转；而配合 `<Switch>` 使用时，**只有当没有路由匹配的时候**，才会进行重定向。 （eg： 跳转-> /error  未定义重定向 -> /）

4. v4版本废弃掉`<IndexRoute>`使用`<Route>`中的`exact`关键词代替

### 3. 使用嵌套路由

第一种方式（不推荐）

这种方式很冗余，渲染时要把整体通用部分重复渲染，项目较大会产生重复代码，降低性能

```jsx
const App = () => (
  <Router>
    <Switch>
      {/* exact 只对当前路由匹配 */}
      <Route exact path="/" component={ Index }></Route>
      <Route path="/other" exact component={ Other }></Route>
      <Route path="/other/:userId" component={ OtherUser }></Route>
      <Route path="/add" exact component={ Add }></Route>
      <Route path="/add/:num" component={ AddNum }></Route>
      {/* 重定向  输入不存在的路径时跳转 */}
      <Redirect to="/" />
    </Switch>
  </Router>
)
```

第二种方式(推荐)

通过组件的思想来实现，对应的路由嵌套到对应的页面。可以使用 `match` 路由属性来优化，方便代码维护

```jsx
const App = () => (
  <Router>
    <Switch>
      {/* exact 只对当前路由匹配 */}
      <Route exact path="/" component={ Index }></Route>
      <Route path="/other" exact component={ Other }></Route>
      {/* 重定向  输入不存在的路径时跳转 */}
      <Redirect to="/" />
    </Switch>
  </Router>
)

const Other = ({match}) => (
  <div>
    <Switch>
      <Route path={match.path} exact render={() => <h3>地址栏输入ID</h3> />
      <Route path={`${match.path}/:id`} component={ User } />
    </Switch>
  </div>
)

const User = ({match}) => (
  <div>
    user id {match.params.id}
  </div>
)
```

***
