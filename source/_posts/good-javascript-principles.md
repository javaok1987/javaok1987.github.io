---
title: Good javascript principles
date: 2017-09-01 16:28:25
banner: /images/javascript.png
tags:
  - js
  - tips
categories: Front-end
---

記錄一些平常開發應該注意的小地方...

<!-- more -->

1.  使用 var 關鍵字宣告變數
未宣告的變數會導致建立一個全域變數。

1.  使用 `===`，而不是 `==`
==（或!=）操作符在需要的時候會自動執行類型轉換，
===（或!==）操作不會執行任何轉換，而且在速度上也比較快。

1.  使用 `for()` 替代 `for-in` 循環
for-in 會在每次跑循環時重算數據組的長度，執行效率較慢。
``` js
for (var i = Array.length - 1; i >= 0; i--) {...}
```
1.  避免使用 `eval()`
使用 eval 是非常昂貴的操作，且也會有安全性問題。

1.  避免在循環內部使用 `try-catch`
把 try-catch 語句放在循環外面，避免每次都要執行它們。

1.  在呼叫 `setTimeout()` 和 `setInterval()` 的時候傳入函式
將函數的引用作為參數傳遞到 setTimeout() 和 setInterval() 裡 `setTimeout(someFunc, 1000)`，
優於將函數名作為字符串參數傳遞 `setTimeout('someFunc()', 1000)`。

...to be continued
