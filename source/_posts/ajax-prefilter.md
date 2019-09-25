---
title: 防止 jQuery 重複提交 ajax 請求
date: 2018-05-31 13:46:32
banner: /images/can_you_repeat_your_question.jpg
tags:
  - js
  - jQuery
  - tips
  - ajax
categories: jQuery
---

jQuery.ajaxPrefilter() 是 jQuery 中的 Ajax 前置過濾器，可以用來前置處理關於 Ajax 的相關設定 (option).

<!-- more -->

#### sample code
``` js
var pendingRequests = {};
// 所有ajax請求的通用前置filter
$.ajaxPrefilter(function( options, originalOptions, jqXHR ) {

    var key = options.url;

    // 請求是否已經存在.
    if (!pendingRequests[key]) {
        pendingRequests[key] = jqXHR;
    }else{
        //如果ajax請求已經存在，下一次相同的請求則取消，防止重複請求
        // 1. 放棄後觸發的提交
        jqXHR.abort();
        // or
        // 2. 放棄先觸發的提交
        //pendingRequests[key].abort();  
    }

    // ajax請求完成時，從臨時對象中清除請求對應的數據.
    var complete = options.complete;
    options.complete = function(jqXHR, textStatus) {
        pendingRequests[key] = null;
        if ($.isFunction(complete)) {
        complete.apply(this, arguments);
        }
    };
});
```

<div class="tip">
捕捉 abort 的異常信息
</div>

``` js
var ajax = $.ajax({
    'error':function(jqXHR, textStatus, errorThrown){
        if(errorThrown != 'abort'){
            //ajax被調用abort後執行的方法
            alert('您的ajax方法被停止了');
        }
    }
})
```

---------------------------------------

#### 參考資料
* [jQuery.ajaxPrefilter()](http://api.jquery.com/jquery.ajaxprefilter/)
* [jQuery如何防止Ajax重複提交](https://www.oudahe.com/p/1283/)
* [防止重複發送 Ajax 請求的解決方案](http://www.hollischuang.com/archives/931)
