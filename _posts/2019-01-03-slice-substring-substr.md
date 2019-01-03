---
title: slice substring substr
excerpt: js 字符串方法 slice substring substr 比较
tags: string js
---

#### 语法

- `slice(start [,stop])`
- `substring(start [,stop])`
- `substr(start [,length])`


#### 相同点

1. 第二个参数都是**可选的**，若省略则默认为字符串结尾处
2. 返回值都是一个**新**的字符串，源字符串不受影响
3. 返回值不包括 **stop** 位置处的字符
4. 若 start 或 stop 为非负数，则该参数规定的是从字符串的**头部**开始算起的位置（从 0 开始）
5. 若 start 或 stop 为负数，则该参数规定的是从字符串的**尾部**开始算起的位置（例如：-1 指字符串的最后一个字符，-2 指倒数第二个字符，以此类推）
6. 参数都必须是数值


#### 不同点

1. slice 的 start 和 stop 参数都可以是**负数**，substr 的 start 参数也可以是负数，substring 的参数只能是**非负**整数
2. substring 如果 start 比 stop 大，在提取子串之前会先**交换**这两个参数的位置
3. substr 是根据**长度**来获取子串，而另外两个方法是按索引位置来获取子串

#### 实例

```javascript
let s = '字符串方法测试'

s.slice(1,4)        // "符串方"
s.substring(1,4)    // "符串方"
s.substr(1,4)       // "符串方法"

s.slice(-4,4)       // "方"
s.substring(-4,4)   // "字符串方"（start 是负数，不符合要求，所以被变更为了 0）
s.substring(4,1)    // "符串方"（stop > start，两个参数交换位置，变成 start=1 stop=4）
s.substr(-4,4)      // "方法测试"
```
