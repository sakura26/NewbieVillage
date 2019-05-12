Challenge Lv1
=====
## 任務目標

* 以純HTML完成一個網頁介紹你最喜歡的作品（小說/漫畫/電影...）
  * 請插入至少一張圖片
  * 程式碼需推上Github
  * **檢查點：給我網址**
* 同上，以Markdown語言做相同的事
  * 程式碼需推上Github
  * **檢查點：給我網址**
* 在Linux(Ubuntu)上安裝Ruby & Rails環境
  * [安裝指引](https://railsbook.tw/chapters/02-environment-setup.html)
  * **檢查點：給我截圖**
* 完成Ruby的“Hello World”初體驗
  * [指引](https://www.ruby-lang.org/zh_tw/documentation/quickstart/)
  * **檢查點：給我截圖**

## Tips

### Linux權限

* ubuntu預設的權限是一般使用者，也就是你使用帳戶登進去的權限，可以做一些寫code、下載檔案之類的行為。
* 而有一個最大權限的帳戶叫root, 跟神一樣可以為所欲為。root這個帳號權限太可怕了，很容易引發一些災難，例如不小心手滑大陸就少一半或世界就毀滅了，所以一般不允許root身份登入
* 取而代之的是，使用sudo命令，這個命令可以允許你使用root的權限去做事，每次做這些事的時候都打入sudo是一種警醒，避免自己做出危險的行為
* 而大多數的程式安裝都需要root身份，因為諸如系統共用函式庫 /lib 之類的地方都等同於只有神才有權限的造陸工程
* 所以，假設原本 bash install.sh 告訴你權限不足，有時改成 sudo bash install.sh就可以了
* 而一般安裝命令的說明會告訴你該用什麼身份來執行，如果他告訴你要用root身份卻沒有在指令前面加sudo, 自己加上去就是了

### 安裝Ruby

* 安裝的指令不難，大致上如同指引所述，不過有一點要留意：安裝到rvm的地方的時候他可能會跟你抱怨gpg憑證匯不進去或無法編譯native-gem。如果你遇到相同的問題，這麼做：

```
# 安裝系統套件
$ sudo apt install -y build-essential zlib1g-dev ruby-dev sqlite3 libsqlite3-dev libssl-dev libreadline-dev libyaml-dev libcurl4-openssl-dev curl git-core python-software-properties nodejs
# 安裝MySQL資料庫（這邊會問你資料庫的密碼）
$ sudo apt -y install mysql-server mysql-client libmysqlclient-dev
# 匯入金鑰
$ gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
# 安裝 rvm
$ \curl -sSL https://get.rvm.io | bash -s stable
# 安裝 rails
$ sudo gem install rails
```

* 注意前面的 # 與 $ 符號，這代表了目前這個命令是以什麼身份執行的，一般身份會顯示為 $, 特權身份則為 # ，算是閱讀指引時的一個hint, 不要直接整段複製去執行囉。你會注意到特權身份的 # 本身也代表了註解，這是為了怕有人不小心貼上跑了指令把東西搞壞了
* 每個命令執行都會從螢幕上得到一串回覆訊息，這些內容很重要最好閱讀過，尤其是尋找裡面有Error / Fatal / failed之類的語句，他會告訴你什麼地方出了問題，然後你就可以去Google找解答。很多時候命令是彼此相依的，中間失敗了下面就一起噴掉了
* 建立專案的時候，他可能會跟你要求指定版本的ruby與安裝套件```bundle install```

### 關於Linux命令

* 有些時候你會不知道一個命令是做什麼的，或是他有哪些參數可以用，例如你想印出rails的版本編號。
* Linux裡面一般有幾個方式你可以去查詢，man的命令讓你查詢特定指令的用法，而多數命令有內建--help參數來讓你查詢用法，例如
  * ```man rails ```
  * ```rails -v```
* 當然，直接去Google也是個好辦法，不過偶而你會發現它給你的方法不一定work, 因為版本不同支援的參數也可能不同，這個時候回頭用man還是比較保險的

### HTML的幾個常見問題

* 一般來說html檔案會以.html為副檔名，或是.htm, 雖然推薦用完整的.html
* 你可能會想我寫的這個html檔該放到哪去，我會建議你把檔案放到你的git專案目錄下，用git命令推上去之後再給我連結。不是很建議你直接在github的頁面上修改，他會模擬你的身份去做git操作，然後就變成一個github上的版本跟你電腦上不一致，你下次git命令就會跟你抱怨要你做pull跟merge了，多一個麻煩
* html / head / body 標籤是很重要的基礎結構，而且一般一個網頁只允許一組，不要交錯或放錯位置了
* 標籤結構長得像這樣 ```<tag arg1="aaa" arg2=123>``` ，如果參數內文是字串就用" "匡起來，數字則不用筐。標籤名稱與可以使用哪些參數請參照html定義
* 標籤務必成對，例如 ```<a href="xxx"> xxx <img src="xxx"></img> </a>```。雖然有少數標籤是允許單一出現的，例如```<hr>```，不過我也會建議用```<hr />```的方式來寫，註明這個標籤依然是成對的只是我不寫出來。
* 引用圖片或連結時避免用到你電腦上的路徑，這樣會導致別人的電腦在看的時候找不到檔案，就一個叉燒包。 錯誤示範：```<img src="D:\Users\admin\Desktop\1.png">```
* HTML是一種巢狀式標籤，每個標籤的使用“不可以交錯”，例如font標籤在這邊橫跨了p標籤就是不合法的
  * 錯誤示範：```<p><font></p><p></p></font>```
  * 正確：```<p><font></font></p> <p><font></font></p>```
* 貼圖的部分，引用了很多別的網站的外部圖片，這樣不是不行，我也會偷懶這麼做。不過正式來說，圖片放在自己的空間比較好，免得別人刪檔案你這邊叉燒包
  * 你可以在git上開一個img資料夾，把下載來的圖片pic.jpg丟進去，然後你就可以用/img/pic.jpg去引用了，可以參考這篇的原始碼
* iframe很好用，不過基於他有一些安全性問題，加上畫面會很醜，我們很少用就是
* 你使用了```<font face="微軟正黑體" color="000000" size="3">```的方式指定字體，這樣很好，不過跟本地圖片有一樣的問題：只有別人有安裝微軟正黑體的電腦才能顯示你預期的樣子。所以我們一般來說有幾種解法：
  * 1.挑windows/mac都有的保險的字體，通通列進去讓電腦自己取挑 
  * 2.進階：使用web字體例如 [google](http://www.flycan.com/article/css/google-fonts-webfont-2474.html) 或 [justfont](https://www.justfont.com) 
  * 3.進階：自己包字體 
  * 4.使用特殊字體的地方通通用圖片處理

### Markdown

* 同HTML, 你可以直接推到Github去，github會主動幫你解釋並呈現
* 你也可以用 [HackMD](https://hackmd.io/) 也很方便，可以線上即時看到編輯的結果
* MD中也可以使用HTML語法，不過我希望你以MD語法為主，畢竟這是一個練習
* 你可以檢視這篇Readme的原始碼來看我怎麼使用的，拉到最上面點選README.md之後右上角有一個“Raw”的按鈕可以按
* 更多的教學 
  * <https://guides.github.com/features/mastering-markdown/>
  * <https://markdown.tw/>
  * <https://www.jianshu.com/p/q81RER>

![](img/lv1_1.png)
