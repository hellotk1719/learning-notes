# Hello, JavaScript！

* [JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)

## jQuery

* [jQuery](https://jquery.com/)
* [jQuery Tutorial](https://www.w3schools.com/jquery/)

**The Document Ready Event**

```javascript
$(document).ready(function() {

    // jQuery methods go here...

});
```

**获取浏览器窗口文档宽高**

```javascript
// 获取浏览器时下窗口可视区域宽度
alert($(window).width());
// 获取浏览器时下窗口可视区域高度
alert($(window).height());

// 获取浏览器时下窗口文档的宽度
alert($(document).width());
// 获取浏览器时下窗口文档的高度
alert($(document).height());

// 获取浏览器时下窗口文档 body 的宽度
alert($(document.body).width());
// 获取浏览器时下窗口文档 body 的高度
alert($(document.body).height());

// 获取浏览器时下窗口文档 body 的总宽度，包括 border、padding、margin
alert($(document.body).outerWidth(true));
// 获取浏览器时下窗口文档 body 的总高度，包括 border、padding、margin
alert($(document.body).outerHeight(true));

// 获取滚动条到顶部的垂直高度
alert($(document).scrollTop());
// 获取滚动条到左边的垂直宽度
alert($(document).scrollLeft());
```
