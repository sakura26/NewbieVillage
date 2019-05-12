Challenge Lv3
=====
## 任務目標

* 製作一個RoR網頁，實現「輸入email訂閱電子報」的功能，輸入的email將會儲存於Server上的/tmp/emaildump.txt中，並有一頁可以顯示目前儲存的所有email
  * 考驗的是：建立基礎RoR專案、使用HTML表單傳送與接收使用者的輸入、用Ruby寫入與讀取文字檔案
  * 進階：儲存時檢查輸入的email格式是否正確、是否重複
  * 進階：顯示所有email的時候允許使用者對email進行排序（使用bootstrap的表格模組實現），並有一欄勾選框允許使用者刪除任意多行email(刪除功能於RoR實現)
  * 程式碼需推上Github
  * **檢查點：給我網址**
* 使用Bootstrap把Lv1「介紹你最喜歡的作品」的網頁改寫
  * [指引](http://www.runoob.com/bootstrap/bootstrap-tutorial.html)
  * 程式碼需推上Github
  * **檢查點：給我網址**

## Tips

### 關於Ruby的手動測試

* 教學中最基本的執行Ruby的方式，就是寫成一個檔案，然後使用```# ruby xxx.rb``` 的方式去執行，然後看輸出結果，不過有時程式大一點的時候會不太直覺，你得一次寫完，確認語法都對，執行了才知道中間的邏輯有沒有錯
* 另一種方案，你可以使用irb這個命令。
  * https://www.ruby-lang.org/zh_tw/documentation/quickstart/

### 常見的程式除錯法

* 大致上有幾種風格的程式除錯，一種是仰賴IDE開發工具，讓他幫你逐步執行，你可以在過程中看到所有變數目前的數值，以及每一行執行後發生了什麼事，甚至可以當下修改它，不過sublime並不支援這種模式
* 另一種模式是比較老派的，在你覺得有問題的地方，前面把變數印出來，執行後再把變數印出來，比對一下改變是不是跟你預期的一致。或是如果你不確定這一個分支有沒有被執行到，就在裡面加一行```puts "it happens!"```，如果你看到他，就代表這個分支進去了。我自己是很常放```puts "WTF happens: function main exception xxxx"```在程式碼裡面去追蹤那些不該發生的狀況

### 關於Rails

* Rails本身是一個框架，它的作用在於讓你寫網站的時候更加簡潔，不用什麼都自己重新刻。不過反過來，如果你沒有先理解他的架構，會各種一頭霧水ＸＤ
* Rails的核心概念是MVC架構，這非常重要，我們下面會簡介
* 一般來說基礎用法是，
  * 先使用```# rails new <專案名稱>```建立一個新專案的骨架，然後根據裡面的目錄結構，
  * 先去Routing定義你的網站流程（使用者該怎麼走），
  * 去Model定義你的資料結構，
  * 到Controller寫你的程式邏輯，
  * 把網頁呈現放到View裡，
  * 靜態網頁則丟到Public去，
  * 一切都準備好了，用這個命令啟動你的專案```$ bin/rails server```
* [Rails幫你預先建立的專案的檔案結構](https://rails.ruby.tw/getting_started.html)
* [Wiki的介紹](https://zh.wikipedia.org/wiki/Ruby_on_Rails)


### MVC架構
![](https://railsbook.tw/images/chapter10/mvc.png)

* 基本上MVC是一種設計模式，讓你簡化你的思路，避免遇到問題。雖然直覺來說網站就是 使用者發送Request去給伺服器要求資源 -> 伺服器回應處理結果，但是這樣中間有不少問題存在，讓我們講點歷史...

  * 最原始的網站開發，以php為例，就是所有的東西都寫在同一個php檔裡面，裡面有一堆if else來判斷，收到什麼request, 要做什麼事，要回傳什麼結果。在小程式的時候這最簡單，東西都集中，但是當程式長大的時候，馬上遇到幾個副作用：程式與HTML亂成一團、網頁畫面只能靠想像，沒辦法丟去瀏覽器看，以及改寫的時候很難寫
  
  * 所以大家開始鼓吹要把不同用途的程式拆開來，例如留言板可能會拆成 view.php, list.php, msg.php, new_post.php, delete_post.php等等好幾個，雖然URL也變成了好幾個，不過至少沒那麼亂了。你可以注意到，這個時候 list.php, view.php, msg.php就是專門顯示的，new_post.php, delete_post.php則專門執行動作，執行完之後轉送給顯示的php, 這正是Controller 與 View的概念：前者做事，後者顯示
  
  * 不過還有一個問題在。由於每個檔案都拆開了，所以遇到一點問題：我怎麼把Controller的結果傳遞給View? 我怎麼知道哪些是正確的進入點（Controller）？如果我的功能是需要使用者登入的，我每個Controller都需要加上相同的程式碼去檢查登入，但是如果我改版的時候漏了改某一支程式，那可能就變成安全漏洞了。看起來把東西都拆開來也是有不少問題，那怎麼辦呢？
  
  * 所謂分久必合合久必分，所以出現了一個叫Routing的東西把所有入口集中起來。Routing本身是一個入口與一張表格，紀錄了什麼Request要轉交給什麼地方，他收到使用者的Request之後會先做一些檢查過濾，例如檢查用戶權限，然後轉送到對應的Controller，例如如果是admin權限就執行刪除，如果是一般用戶權限顯示錯誤訊息，如果還沒登入就轉向登入頁面。有了這個，網站變得好控管許多，Controller專心做他的任務就好
  
  * 那麼，Model是什麼呢？一般來說我們儲存數據，可能是使用MySQL之類的資料庫，或是其他方式。但是MySQL執行SQL語法本身不是那麼直覺，他是表格，而不是一般程式設計師常用的物件導向。同時SQL語法散佈在不同的Controller裡面也有一些缺點：又臭又長，安全性控管不好掌握，哪一天要換資料庫的時候更是一場災難... 因此，MVC架構提出了一種新的思路：ORM, 我把這些資料儲存操作也封裝成物件，由Model幫你處理後面的對應，你只需要生成物件跟修改物件就好！從此之後的用法從到處都寫SQL, 變成 搜尋Model、取得物件、修改物件、儲存，讓操作簡單許多。至此，MVC架構的概觀已經成形
  * ORM在Rails上被稱為ActiveRecord，你要定義幾件事：要使用哪一種資料庫？資料庫的帳號密碼？要儲存哪些類型的物件？每種類型的物件中有哪些屬性？這些資料被定義在Model的檔案中，你的Controller與Routing就可以直接引用。雖然你看教學中有不少什麼一對一多對一好像很複雜的關係，不過以目前來說，你也可以不建立關聯，直接使用。
  
* [MVC介紹](https://railsbook.tw/chapters/10-mvc.html)
* [MVC另一個介紹](https://zh.wikipedia.org/zh-tw/MVC)
* [Rails的ORM: ActiveRecord](https://ihower.tw/rails/activerecord.html)
* ORM還是基於SQL的概念，所以學會SQL架構還是很重要的。只是這玩意也是挺不簡單的...我會推薦找本書，或是找門課程來上，作為未來進修 [SQL入門](https://www.1keydata.com/tw/sql/sql.html)

### 在Server/Client端的常見除錯法

* 我們剛剛介紹了Ruby的除錯法，但是在Rails架構下，我印出來的東西該上哪邊去看呢？直覺是把內容直接輸出到Client的瀏覽器上，但是有些時候出錯了，程式直接掛掉來不及顯示到Client端這招就無效了
* 不過，把東西印到Console(puts)總是有用的，只是你可能不知道他印到哪邊。在你啟動Rails的那個指令介面，事實上他會持續運作，並把你印出的內容輸出到螢幕上，那邊是很好的一個參考點。當然，也許你不是那麼方便看到原本的Console, 但你也可以到該專案的log目錄下，那邊會留下所有的紀錄。你可以使用linux命令```# tail -f <log file>```來即時監控目前的數據狀況
* 另一種方式是，把數據導向到所有linux統一紀錄log的地方：syslog也是很不錯的方法，[官方API](https://ruby-doc.org/stdlib-2.2.3/libdoc/syslog/rdoc/Syslog/Logger.html)
