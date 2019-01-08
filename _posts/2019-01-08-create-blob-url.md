---
title: Create url for input[file]
excerpt:  本地文件转 blob/base64
tags: js file url blob base64
---

#### 获取本地文件 blob 格式 url
```javascript
function getObjectURL(file) {
  var url = null;
  if (window.createObjcectURL != undefined) {
    url = window.createOjcectURL(file);
  } else if (window.URL != undefined) {
    url = window.URL.createObjectURL(file);
  } else if (window.webkitURL != undefined) {
    url = window.webkitURL.createObjectURL(file);
  }
  return url;
}
```

#### 图片预览：base64 格式

```html
<input type="file" id="inputBox" >
<img src="" id="img">
```

```javascript
var inputBox = document.getElementById("inputBox");
var img = document.getElementById("img");
inputBox.addEventListener("change",function(){
  var reader = new FileReader();
  reader.readAsDataURL(inputBox.files[0]);
  reader.onload = function(){
    img.src = this.result
  }
})
```
