---
title: 测试文章
tags:
  - JS
  - Javascript
categories: web前端
---

### 定时器
```javascript
function showSnackbar() {
  var $snackbar = $("#snackbar");
  $snackbar.addClass("show");
  setTimeout(() => {
    $snackbar.removeClass("show");
  }, 3000);
}
```
