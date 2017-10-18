---
title: Responsive Web Design (RWD) 和 Adaptive Web Design (AWD)
tags: [RWD, AWD, 自適應網頁設計, Media Queries]
date: 2017-10-18 12:00:00
banner: /images/rwd.jpg
categories: Web
---
`RWD` 和 `AWD` 的出現都是由於移動上網設備日益普及，針對不同設備(尤其考慮不同屏幕尺寸)及其使用條件(通常有比較低的頻寬，流量和性能等) 對網頁作出優化，以帶來更好的用戶體驗。
<!-- more -->

### Responsive Website Design (RWD，自適應網頁設計)
  在 Client 端偵測瀏覽器視窗大小，配合如流體佈局和可以自適應的圖片/視頻等技術，使頁面只需同一套程式碼，就能夠適應不同屏幕尺寸的技術。

  但由於單一網頁內要處理各種尺寸裝置的關係，必須包含所有版型需要的資源，網頁檔案會較肥大；或者是小螢幕卻用高解析度的圖檔顯示，導致下載速度過慢。

### Adaptive Web Design (AWD)
  經由 Server 端判斷來源後，針對不同的 Client 設備來增減內容和外觀以提高適應性和用戶體驗。這種方式可以針對個別裝置設計單獨的資源。例如針對小螢幕設計的 HTML 檔、低解析度的圖檔...等等，檔案內容不必包山包海，下載速度較快。

  但也也為要針對不同裝置設計不同的流程，相對起來相對費工。

<div class="tip">
     可以在這個網站 [Liquidapsive](http://www.liquidapsive.com/) 切換 RWD、AWD、Liquid、Static...等四種不同 layout 效果。
</div>


#### 參考資料
* [Liquidapsive (Liqui-dap-sive)](http://www.liquidapsive.com/)
* [Responsive Web Design (RWD) 和 Adaptive Web Design (AWD)](http://www.xenyomedia.com/blog/134/responsive-web-design-rwd-%E5%92%8C-adaptive-web-design-awd)
* [[摘要]Combining Responsive and Adaptive Strategies to Solve Mobile Design Challenges](http://iki0723.blogspot.tw/2012/11/combining-responsive-and-adaptive.html)
