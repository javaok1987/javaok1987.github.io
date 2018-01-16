---
title: CSS Note
date: 2017-09-05 11:40:14
banner: /images/css.gif
tags:
  - css
  - tips
categories: Web
---

整理一些常常用到的 css 語法，方便之後切版使用。

<!-- more -->

1.  清單項目分隔線
在清單項目之間使用框線做分隔，用 item + item 避開第一個項目。
``` css
li + li { border-top: 1px solid black; }
```

1.  圖片取代文字
因為瀏覽器會去渲染超大的寬度，所以不使用 `text-indent:-9999px;`語法，改用下列語法以增加效能。
``` css
.hide-text {
  text-indent: 100%;
  white-space: nowrap;
  overflow: hidden;
}
```
  > 參考資料
  [REPLACING THE -9999PX HACK](http://www.zeldman.com/2012/03/01/replacing-the-9999px-hack-new-image-replacement/)
