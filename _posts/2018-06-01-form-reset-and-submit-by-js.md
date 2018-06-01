---
title: 'form-reset-and-submit-by-js'
excerpt: '解决用 js 提交/重置表单时报错：submit/reset is not a function'
---

### 解决用 js 提交/重置表单时报错：submit/reset is not a function

参考链接：
- [Form resetting is not working](https://stackoverflow.com/a/20286263)

#### 1. 表单 html 结构

```html
<form id="ajaxForm">  
  <input type="text" name="username">
  <input type="password" name="password"> 
  <input type="submit" id="submit" name="submit" value="Submit">  
  <input type="reset" id="reset" name="reset" value="Reset">  
</form>
```

#### 2. js 提交/重置表单的方法

```javascript
// 由于 submit 和 reset 方法都是定义在 HTMLFormElement 上的，
// jQUery 中并没有这两个方法，所以需要获取到表单 DOM 对象
// 原生 JavaScript 
let form = document.getElementById('form')
// jQuery
// let form = $('#form')[0]

// 提交
form.submit()

// 重置
form.reset()
```


但是，使用上面的 html 结构 和 js 代码来操作表单，会报错 `form.submit is not a function`

此时，控制台打印 `form.submit`，发现输出的是 `<input type="submit" id="submit" name="submit" value="Submit">  `

报错原因就在这里：给 input 按钮设置的 `id="submit"` 或者 `name="submit"` 都会导致表单的 `submit()` 方法被覆盖，
导致调用 `form.submit` 获取到的是这个 `<input id="submit">` 元素，而不是原本定义的 `submit()` 方法

#### 3. 解决方案

不要把提交、重置按钮的 id 和 name 属性设置为 submit 和 reset 即可，例如：
```html
 <input type="submit" id="submitBtn" name="submitBtn" value="Submit">  
 <input type="reset" id="resetBtn" name="resetBtn" value="Reset">  
```

