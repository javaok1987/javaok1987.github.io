---
title: Get URL Parameters with JavaScript
date: 2018-01-16 11:30:00
banner: /images/pov-3046269_1280.jpg
tags:
  - js
  - jquery
  - querystring
categories: Web
---
擷取網址列所帶參數
<!-- more -->

### JavaScript Pure:
``` js
function getParameterByName(name, url) {
    if (!url) url = window.location.href;
    name = name.replace(/[\[\]]/g, "\\$&");
    var regex = new RegExp("[?&]" + name + "(=([^&#]*)|&|#|$)"),
        results = regex.exec(url);
    if (!results) return null;
    if (!results[2]) return '';
    return decodeURIComponent(results[2].replace(/\+/g, " "));
}
```
#### Usage:
``` js
// query string: ?foo=lorem&bar=&baz
var foo = getParameterByName('foo'); // "lorem"
var bar = getParameterByName('bar'); // "" (present with empty value)
var baz = getParameterByName('baz'); // "" (present with no value)
var qux = getParameterByName('qux'); // null (absent)
```

### ES2015 (ES6)
``` js
const getParams = query => {
  if (!query) {
    return { };
  }

  return (/^[?#]/.test(query) ? query.slice(1) : query)
    .split('&')
    .reduce((params, param) => {
      let [ key, value ] = param.split('=');
      params[key] = value ? decodeURIComponent(value.replace(/\+/g, ' ')) : '';
      return params;
    }, { });
};
```
#### Usage:
``` json
// query string: ?foo=lorem&bar=&baz
{"foo": "lorem", "bar": "", "baz": ""}
```

### JQuery Plugin:
``` js
(function($) {
    $.QueryString = (function(paramsArray) {
        let params = {};
        for (let i = 0; i < paramsArray.length; ++i){
            let param = paramsArray[i].split('=', 2);
            if (param.length !== 2)continue;
            params[param[0]] = decodeURIComponent(param[1].replace(/\+/g, " "));
        }
        return params;
    })(window.location.search.substr(1).split('&'))
})(jQuery);
```
#### Usage:
``` js
// query string: ?foo=aaa&bar=&baz
var foo = $.QueryString['foo']; // "lorem"
var bar = $.QueryString['bar']; // undefined
alert(foo);
```

### URLSearchParams API:
``` JS
let params = new URL('https://example.com?foo=1&bar=2').searchParams;
params.get('foo'); // "1"
params.get('bar'); // "2"
```
<div class="tip">
  Browser support:
  ![URLSearchParams API](/images/URLSearchParams_API_support.png)
</div>

### Clean QueryString
``` JS
const removeQueryString = () => {
  window.history.history.pushState('', document.title, window.location.pathname);
}
```

#### 參考資料
* [How can I get query string values in JavaScript?](https://stackoverflow.com/questions/901115/how-can-i-get-query-string-values-in-javascript)
* [URLSearchParams API ](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams)
