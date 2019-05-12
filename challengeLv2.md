Challenge Lv2
=====
## 任務目標

* 製作一個網頁，請用JavaScript/jQuery加入「輸入生日，計算年齡，未滿18歲送去迪士尼」的功能
  * 考驗的是 使用jQuery的能力 字串解析、日期換算、重新導向等。你也可以單純利用JavaScript來實現這個功能。你也會想看一下HTML的表單
  * 進一步，你可以使用Bootstrap的模組 [Datepicker](https://jqueryui.com/datepicker/) 來讓使用者輸入日期更簡便
  * 程式碼需推上Github
  * **檢查點：給我網址**
* 完成RoR的“Hello World”初體驗
  * [指引](https://ihower.tw/rails/firststep.html)
  * 程式碼需推上Github
  * **檢查點：給我網址**
* 把Lv1「介紹你最喜歡的作品」用CSS裝飾得更美觀
  * 程式碼需推上Github
  * **檢查點：給我網址**
* 新增任務：設置Github pages, 以後交前端作業請都以此繳交
  * [教學](https://gitbook.tw/chapters/github/using-github-pages.html)
  * **檢查點：用妳的github pages繳交作業**

## Tips

### 關於HTML，進階一點

* 還記得HTML的表單吧？定義一個form, 然後裡面可以有多個輸入欄，然後有一個reset跟一個submit按鈕
* 如果你只是表單不要做操作，Datepicker使用者點完之後出現那個數值就已經在欄位裡了，送出就會跟著送出去。而如果你要拿這個欄位裡的數值，請參照jquery（基本上javascript就可以拿了，不過jquery比較簡單一點）
* HTML的核心都在DOM物件，大部分的資訊也都儲存在DOM裡面。基本上你在HTML中寫個每一個文字、標籤什麼的，都會轉換成DOM物件被放置在網頁上。
* 你可以想像HTML是網頁的設計圖，而瀏覽器會幫你像蓋房子一樣生成DOM物件放在頁面上，最終疊成你看到的樣子

### 關於網站與使用者（HTTP Server/Client架構）

* 當使用者打開一個網頁時，實際上發生的事情是這樣的
* 使用者在瀏覽器上輸入網址，瀏覽器透過網址的URL，查詢DNS, 找到Server的IP位址進行連線
* URL長這樣 http://www.ccsakura-net.com/index.htm ，可以拆成幾個元素
  * 使用http通訊協定（未加密）
  * 主機位址在www.ccsakura-net.com，透過DNS查詢 => 140.121.80.29
  * 跟主機要求的URI是 /index.htm ，一般是對應到檔案，在MVC架構中則是指引Routing的關鍵字（參閱Lv3 MVC）
* 瀏覽器連到Server，把主機位址、URI與一些瀏覽器端（Client）的資料發送給Server
* Server接收到，交給對應的程式處理之後，將回應發回給Client端，以這個例子，就是把網站根目錄下的index.htm直接送回給Client
* [參考](https://medium.com/@justinlee_78563/%E9%97%9C%E6%96%BCweb%E5%BE%8C%E7%AB%AF-1-%E4%BB%80%E9%BA%BC%E6%98%AFweb-server-83ee32bc7d3e)

