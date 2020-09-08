---
title: JS骚操作
date: 2020-07-03 14:21:37
tags: [javascript]
---

看见大佬们的代码，总结和搬运了些骚操作

<!-- more -->

## 位运算操作

1. 左移运算符快速算出2的次方

    ```javascript
    1 << 2 // 4  2的2次方
    1 << 10 // 1024 2的10次方
    /* !注意 */
    1 << 32 // -2147483648 超出精度
    ```

2. 使用 `^` 切换变量 0 或 1

    ```javascript
    // 三目运算
    toggle = toggle ? 0 : 1
    // ^
    toggle ^= 1
    ```

3. 使用 `~~` 切换布尔值为 0 或 1

    ```javascript
    ~~true // 1
    ~~false // 0
    ```

4. 使用 `+` 改变string为number

    ```javascript
    +'100' // 100
    ```

5. 使用 `!!` 将数字转为布尔值

    ```javascript
    !!0 // false
    !!2 // true
    ```

6. 使用`~`、`>>`、`<<`、`>>>`、`|`来取整

    ```javascript
    ~~4.51 // 4
    4.51 >> 0 // 4
    4.51 << 0 // 4
    4.51 | 0 // 4
    4.51 >>> 0 // 4 负数无效
    ```

7. 使用 `^` 来完成值交换

    ```javascript
    let a = 7
    let b = 1
    a ^= b
    b ^= a
    a ^= b
    console.log(a, b) // 1, 7

    ES6解构
    [a, b] = [b, a]
    ```

8. 使用 `^` 判断正负数

    ```javascript
    (1 ^ a) > 0 // 为true是正数
    (-1 ^ a) > 0 // 为true是负数
    ```

9. 使用 `^` 来检查数字是否不相等

    ```javascript
    a = 7
    a !== 7 // false
    a ^ 7 // 0
    ```

10. 使用 A + 0.5 | 0 来替代 Math.round()

    ```javascript
    a = 7
    a !== 7 // false
    a ^ 7 // 0
    ```
