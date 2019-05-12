Challenge Lv4
=====
## 任務目標

* 製作一個首頁，使用者輸入暱稱之後下次回來將會顯示該暱稱，同時有一個「忘記我的名字」
  * 考驗的是：使用session記錄使用者資料
  * 程式碼需推上Github
  * **檢查點：給我網址**
* 同Lv3的訂閱電子報，但改將資料儲存於MySQL資料庫中（建立一資料庫Lv3與一資料表email，儲存email、記錄時間、發文者IP三個欄位）
  * 考驗的是：基礎MySQL操作
  * 進階：對email欄位建立Index加速查詢，並以此作為避免重複寫入的方式
  * 進階：儲存時查詢確認email是否重複
  * 進階：允許使用者刪除任意多行email(一次刪除多筆於SQL語法實現)
  * 程式碼需推上Github
  * **檢查點：給我網址**
  
## Tips

### Session初探

<http://fred-zone.blogspot.com/2014/01/web-session.html>

「Session 的機制就像是你去飲料店下了單以後，得到號碼牌，然後你走開幾步，店員就忘了你是誰。所以，如果你想去取飲料，你就得靠這張號碼牌，去跟店員領，店員會跟據這號碼牌，認定你是顧客、是否點過餐、知道你點了什麼東西，然後可以接著給你屬於你的飲料。」

「在最原始的 Session 設計，大多開發者都將資料存在 Server 上，也就是你點了什麼飲料，都是記錄在 Server 裡，可能是 Database、記憶體或是檔案，可以以任何一種形式儲存。然後，當你去領飲料時，店員會輸入你的號碼，用你的號碼得知你是否點過餐、點了什麼東西。」

「Cookie-based Session 就被提出為一個解決方案，把資料暫存放在 Cookie 中，讓 Client 自己負責保存。簡單來說，就是把你點什麼飲料，通通直接寫在號碼牌上。Server 就可以直接看你的號碼牌上寫了什麼，而不必花大量時間去後面建立大規模的 Server 來處理 Session 。」

至於Session存在Server上有另一個延伸，也就是把數據存到資料庫裡面。想像店員只靠腦袋記住你的號碼與內容，結果店員下班換了一個人，或是你跑到分店要去取飲料，對方就不知道你是誰了。資料庫可以長期儲存，就算跨不同分店，或是換了店員，都依然可以記得你。

在Rails的實作上分別對應到以下三種

<https://rails.ruby.tw/action_controller_overview.html>

* ActionDispatch::Session::CookieStore ─ 所有資料都存在用戶端（寫在號碼牌上）
* ActionDispatch::Session::CacheStore ─ 資料存在 Rails 的 Cache（店員用腦袋記住）
* ActionDispatch::Session::ActiveRecordStore ─ 資料使用 Active Record 存在資料庫（需要 activerecord-session_store RubyGem）

用法請參照內文


### Database初探

資料庫，一個Web應用中相當核心的支柱。大致上這是一個很大的主題，雖然要能用不會花太多時間，但要學習的好，這條路是以年為單位來算的。

為什麼要有資料庫呢？我們前面使用過幾種儲存數據的方法

1. 儲存在變數中
2. 儲存在Session中（事實上還是變數）
3. 儲存在文字檔案裡面

都能存，但也都會各有麻煩的情況，諸如

* 變數與Session重開Server就沒了
* 文字檔案中的內容可能有格式問題 - 你預期收到的是timestamp, 結果寫入時不小心塞入了別的東西，然後顯示就壞光光了
* 資料量很大的時候，文字檔案容易壞掉，也不好抓問題
* 如果同一個瞬間有兩個人同時寫入資料於同一個檔案，很容易造成檔案損毀（想像兩個人同時在一張紙的同一個位置寫字，會互相重疊）
* 掃描一份文字檔找資料超慢
* 如果同時有多台Server要用同一份資料，處理起來很麻煩
* 如果數據很複雜要做交互關聯（例如要找出一個使用者做過所有的交易的對象），處理起來會又麻煩又慢

而資料庫有以下幾個特性

* 可以容納大量資料的長期儲存
* 資料格式預先定義好，所以不用擔心讀到的資料格式超乎預期
* 速度快，如果經過適當的調整會更快
* 可以接受同時大量的讀取與寫入不會打架
* 可以多台Server共用同一份資料庫
* 可以幫你自動完成交互關聯（UNION與JOIN）

一台資料庫一般來說可以有好幾個 Database 來讓你儲存許多不同的專案的資料，而每個Database中又可以有很多份Table，每份Table就像一張Excel表格，分成很多不同的欄位(column)，而Table中可以儲存很多的資料行（row）

假設用Excel來理解的話，你的電腦就是一台Database Server, 裡面可以有很多份xls檔案（Database），每份xls中又可以有很多頁籤(Tables)，而頁籤中有標題（columns），以及很多數據(rows)

一般來說，我們會使用網路連線到Database Server去做操作，這樣方便多台Server可以共用同一份資料。當然也有如SQLite這種特別的資料庫是不透過網路的類型

由於是透過網路連線，所以資料庫上一般也會有帳號密碼的認證，來避免任何阿貓阿狗來亂用你的數據。所以別忘了為了你的專案配置一個專屬的帳號

資料庫的使用大致上來說是這樣

1. 在Database Server上create database（此例使用前面讀書會的msgboard）
2. 定義table（此例為posts）的欄位為timestamp（格式為整數int）、email（格式為字串varchar）、nickname（格式為字串varchar）、posttext（格式為字串varchar），另外我們建立一個欄位叫id來作為每篇貼文獨一無二的編號（取代原本使用的timestamp、格式為整數int、並定義為primary key）
3. 使用上面的定義，在database msgboard中建立table posts
4. 配置rails專案的/config/database.yml 中資料庫的位置、名稱與帳號密碼
5. 測試連線
6. 配置Mode把數據模型對應到資料庫上
7. 開始在程式碼中使用資料庫

2,3,5,6事實上可以靠rake命令幫你完成，參見下面參考資料

由於Rails事實上做了不少事情來幫助你操控資料庫，有許多特有的命令與輔助工具如rake，可以看一下 參考資料 [创建第一个 Rails 程序(使用mysql)](http://rubyer.me/blog/231/)

使用方便，記得回頭看一下Rails 的 Models章節

<http://www.codedata.com.tw/database/mysql-tutorial-getting-started>

這篇寫的教學滿完整的，不過有點太多，我們先學習 1-3 就可以初步使用，4-9 學會了就可以做很多事了，11章非常重要一定要學，其他就有空再研究吧

1. 資料庫概論與 MySQL 安裝
2. SELECT 基礎查詢
3. 運算式與函式
4. JOIN 與 UNION 查詢
5. CRUD 與資料維護
6. 字元集與資料庫
7. 儲存引擎與資料型態
8. 表格與索引
9. 子查詢
10. Views
11. Prepared Statements
12. Stored Routines入門
13. Stored Routines的變數與流程
14. Stored Routines進階
15. Triggers
16. 資料庫資訊
17. 錯誤處理與查詢
18. 匯入與匯出資料
19. 效率



