---
title: CSS Note
date: 2017-09-05 11:40:14
banner: /images/css.gif
tags:
  - css
  - tips
categories: CSS
---

整理一些常常用到的 css 語法，方便之後切版使用。

<!-- more -->

1.  清單項目分隔線
在清單項目之間使用框線做分隔，用 item + item 避開第一個項目。
  ``` css
  li + li { border-top: 1px solid black; }
  ```

2.  圖片取代文字
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

3.  溢出文字省略變顯示省略符號 (...)

  ``` css
    overflow : hidden;
    text-overflow : ellipsis;
    white-space : nowrap;
    width : 300px;
  ```

4. Clearfix 清除浮動

  ``` css
    .clearfix:before, .clearfix:after {
    	content:"";
    	display:table;
    }
    .clearfix:after{
    	clear:both;
    	overflow:hidden;
    }
    .clearfix{
        zoom:1;
    }
  ```

5. iOS 的 scroll bar.

  ``` css
  ::-webkit-scrollbar {
      width: 15px;
      height: 15px;
      border-bottom: 1px solid #eee;
      border-top: 1px solid #eee;
  }
  ::-webkit-scrollbar-thumb {
      border-radius: 8px;
      background-color: #C3C3C3;
      border: 2px solid #eee;
  }

  ::-webkit-scrollbar-track {
      -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.2);
  }
  ```
