---
title: Auto click button on page load
date: 2017-10-19 15:01:16
banner: /images/macbook-26132456437.jpg
tags:
  - js
  - jQuery
categories: jQuery
---
在網頁載入時自動按下按鈕或連結，執行 `click` 事件。
<!-- more -->

``` html
<button id="my-button" onclick="alert('je ne veux pas travailler.');"></button>
```

### JQuery
``` js
jQuery(function(){
   jQuery('#my-button').trigger('click');
});
```

or
``` js
jQuery(function(){
   jQuery('#my-button').click();
});
```

### JavaScript Pure:
``` js
document.getElementById('my-button').click();
```
