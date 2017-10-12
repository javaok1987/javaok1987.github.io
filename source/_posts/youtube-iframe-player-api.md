---
title: How to control your YouTube videos - YouTube Player API
date: 2017-10-12 16:51:18
banner: /images/youtube.jpg
tags:
  - js
  - youtube
categories: Web
---
使用 [YouTube Player API](https://developers.google.com/youtube/iframe_api_reference) 控制 `YouTube` 影片，包括自動播放、隱藏按鈕、隱藏影片標題、隱藏 YouTube Logo、循環播放...等。
<!-- more -->

### Step 1. 載入 js

``` html
<div id="player"></div>
```

``` js
var initYoutubeVideo = function(argument) {
  var tag = document.createElement('script');
  tag.src = "https://www.youtube.com/iframe_api";

  var firstScriptTag = document.getElementsByTagName('script')[0];
  firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
};
```

### Step 2. 設定 YouTube 影片參數

``` js
var onYouTubeIframeAPIReady = function() {

  var player = new YT.Player('player', {
    videoId: 'YOUR_VIDEO_ID', // YouTube 影片ID.
    width: 560,               // 播放器寬度 (px).
    height: 316,              // 播放器高度 (px).
    playerVars: {
      rel: 0,                 // 是否顯示片尾推薦影片.
      autoplay: 0,            // 是否在讀取時自動播放影片.
      controls: 1,            // 是否在播放器顯示暫停／播放按鈕.
      showinfo: 0,            // 是否隱藏影片標題.
      modestbranding: 0,      // 是否隱藏 YouTube Logo.
      loop: 0,                // 是否讓影片循環播放.
      fs: 0,                  // 是否隱藏全螢幕按鈕.
      cc_load_policty: 0,     // 是否隱藏字幕.
      iv_load_policy: 3,      // 是否隱藏影片註解.
      autohide: 0             // 是否在播放影片時隱藏影片控制列.
    },
    events: {
      onStateChange: function(event) {
        if (event.data == YT.PlayerState.PLAYING) {
          // 開始播放.
        }
      }
    }
  });
};
```
> 如果要做一些簡單的事件觸發或是監聽事件，可以在 `onStateChange` 裡設定。

#### 參考資料
* [YouTube Player API Reference for iframe Embeds](https://developers.google.com/youtube/iframe_api_reference)
* [How to Embed a YouTube Video with Sound Muted](https://www.labnol.org/internet/embed-mute-youtube-video/29149/)
* [如何嵌入 YouTube 影片設定自動重播、隱藏 Logo 或靜音播放？](https://free.com.tw/embed-a-youtube-video-with-sound-muted/)
