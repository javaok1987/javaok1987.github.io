---
title: Debounce & Throttle Function
date: 2017-08-30 14:42:42
banner: /images/clock-1274699_1920.jpg
tags: [js, debounce, throttle]
categories: Web
---
一般綁定 DOM 事件(`resize`、`scroll`、`mousemove`和`keydown/keyup/keypress`等)的時候，常常會因為事件觸發的太頻繁而導致網頁效能低落。

所以我們可以在事件要執行前加一個控制器，降低事件的觸發頻率，最常使用的就是`debounce` 和 `throttle` 這兩個方法，兩者都是用來控制某個事件在一定時間內執行多少次數，看起來非常相似但又有些不同。
<!-- more -->

### Debounce

__用戶停止某個操作一段時間之後才執行相應的監聽事件__
例如，調整瀏覽器視窗大小的時候，會觸發很多次 `resize` 事件，可以使用 debounce 方法在停止調整視窗大小的時候在去觸發相應功能。

![Debounce](/images/debounce.gif)

#### 造輪子

<div class="tip">
    觸發 -> 記錄觸發時間 -> 上次動作觸發時間大於限制時間 -> 執行動作
</div>


``` js
/**
 * 強制一個事件在某個連續時間段內只執行一次.
 *
 * @param  {function} func        實際要執行的事件
 * @param  {number}   delay       延遲時間，單位是毫秒（ms）
 * @param  {boolean}  immediate   設置為ture時，觸發於開始而不是結束
 * @return {function}             返回客戶呼叫事件
 */
function debounce(func, delay, immediate) {
    var timer;
    return function() {
        var context = this,
            args = arguments;
        var later = function() {
            timer = null;
            if (!immediate) func.apply(context, args);
        };
        var callNow = immediate && !timer;
        clearTimeout(timer);
        timer = setTimeout(later, delay);
        if (callNow) func.apply(context, args);
    };
};
```
> 參數 `immediate`，設定函數在一個時間區間的最開始(`true`)執行，還是最後(`false`)執行。



#### 呼叫方式
``` js
var handleScroll = debounce(function() {
	//  Do fun stuff​.
}, 250);

window.addEventListener('scroll', handleScroll);
```

---------------------------------------

### Throttle

__控制監聽事件固定在每 X 毫秒內執行一次__
例如，不管滑鼠移動(`mousemove`事件)的速度多快，固定在每 250ms 執行一次。

![Throttle](/images/throttle.gif)

#### 造輪子

<div class="tip">
觸發 -> 上次動作執行時間大於限制時間 -> 執行動作，記錄執行時間
</div>

``` js
/**
* 固定事件執行的速率.
*
* @param  {function} func    實際要執行的事件
* @param  {number}   delay   執行間隔，單位是毫秒（ms）
* @return {function}         返回一個「節流」事件
*/
function throttle(func, delay) {
    var last, timer;
    delay || (delay = 250);
    return function() {
        var context = this;
        var args = arguments;
        var now = +new Date();
        if (last && now < last + delay) {
            clearTimeout(timer);
            timer = setTimeout(function() {
                last = now;
                func.apply(context, args);
            }, delay);
        } else {
            last = now;
            func.apply(context, args);
        }
    }
}
```

#### 呼叫方式
``` js
var handleScroll = throttle(function() {
	//  Do fun stuff​.
}, 250);

window.addEventListener('scroll', handleScroll);
```

---------------------------------------

### 使用 Underscore.js 中的 `_.debounce` 和 `_.throttle`


不想重新造輪子的話可以直接使用 [Underscore](http://underscorejs.org/) 或 [Lodash](https://lodash.com/)。

另外可以使用 `Lodash` 的指令列工具，產生只有 `_.debounce` 和 `_.throttle` 的壓縮檔。

```bash
npm i -g lodash-cli
lodash include = debounce, throttle
```

#### 呼叫方式
```js
$(window).on('scroll', _.debounce(doSomething, 250));

$(window).on('scroll', _.throttle(doSomething, 250));
```

---------------------------------------

#### 參考資料
* [Debouncing and Throttling Explained Through Examples](https://css-tricks.com/debouncing-throttling-explained-examples/)
* [javascript-debounce-function](https://davidwalsh.name/javascript-debounce-function)
* [Debounce 和 Throttle 的原理及實現](http://hackll.com/2015/11/19/debounce-and-throttle/)
