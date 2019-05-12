Challenge Lv2.5
=====
## 任務目標

考慮到Lv.3第一關的難度似乎過高了，拆出2.5來簡化一下

* 無限延伸的九九乘法表: 輸入一個數字N，然後生成NN乘法表，例如輸入3，輸出如下（練習迴圈，請while/for各寫一次。你應該要能輸入13然後生成一個13x13的大表）
  
```
0|1,2,3
-------
1|1,2,3
2|2,4,6
3|3,6,9
```

* 輸入N行文字，如果文字是END則程式停止接收輸入，將前面收到的輸入轉換成HTML表格輸出。你應該要能處理任意行數，而非只有三行（練習變數/陣列）

```
$ ruby text2html.rb
> abc
> def
> ghi
> END
<table>
<tr><td>1</td><td>abc</td></tr>
<tr><td>2</td><td>def</td></tr>
<tr><td>3</td><td>ghi</td></tr>
</table>
```

* 寫一個Ruby的程式，輸入檔案路徑，印出該檔案前十行。若檔案不存在，印出錯誤訊息，例如 （練習檔案操作）

```
$ ruby lv25-1.rb
What file you want to print?
> /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
```
    * [參考資料](https://ruby-doc.org/docs/ruby-doc-bundle/Tutorial/part_02/user_input.html)
  * 進階：從Command Line參數取得檔案路徑，例如（練習讀入指令行參數）

```
$ ruby lv25-11.rb /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
```
  * 進階：加入“把輸出改存到/tmp/head.txt”的功能，並可以從Command Line指定這個功能是否要啟動（練習讀入指令行參數，以及現代化的參數使用法）
  
```
$ ruby lv25-12.rb --saveto /tmp/head.txt /etc/passwd
```
* 玩轉字串轉換
  * 告訴我 ```123456``` 經過 MD5 Hash / SHA1 Hash / Base64Encode / URLEncode 之後的結果
  * 告訴我 ```aHR0cHM6Ly9naXRodWIuY29tL3Nha3VyYTI2L05ld2JpZVZpbGxhZ2U=``` 原本代表什麼意思呢？
  * 你有沒有辦法把 MD5過的字串 ```5f4dcc3b5aa765d61d8327deb882cf99``` 變回原本的文字呢？如果能是什麼？如果不能，為什麼？
* 表單操作
  * 寫一個簡單的RoR專案，首頁是一個簡易塗鴉牆，有一行的輸入框，以及一個表格。每次輸入送出後，表格內容就會換成輸入的文字
  * 把表格內每次輸入的文字也變成文字輸入框，讓每次送出時，表格內的資料也會一起送到Server，並且再一次顯示出來
  * 進階：表格內增加一個checkbox, 讓使用者可以選擇哪些訊息要刪除
  * 進階：我們不希望使用者可以修改以前輸入的內容，你可以使用「欄位禁止修改」或「隱藏欄位」來做到這件事嗎？

## Tips

### 關於檔案操作

* 檔案操作是所有程式語言幾乎都有的基礎，一般至少會有 新增、讀取、寫入、刪除、列表、檔案資訊 等操作。多數物件導向語言的用法會是：給一個路徑來建立檔案物件，然後對這個物件做操作，例如寫入時會先打開它(open)，然後寫入或讀取資訊，用完了之後要關起來(close)告訴系統你不再使用了。
* 之所以會這麼費事要打開跟關起來，主要是跟系統說你要使用它了，讓他分配相對應的資源給你。關起來之前我們往往會先flush告訴系統把暫存的內容都寫入，然後就不再使用了。
* 一般最基礎的檔案讀取都是read bytes, 呼叫一次這個方法，給他一個bytes陣列，他就會把這個陣列填滿，並回傳說他讀了多少個bytes你可以用。只不過這個方法實在不是很便利，又要自己算緩衝又要轉換成字串麻煩的很，所以也推出了如一次讀取整個檔案成字串，或是一次讀取一行的API可以用。
* 如果檔案不大，一次讀取整個之後再自己用字串切割（例如split）也是挺方便的，只是如果遇到大檔案，有可能會讀取失敗（記憶體塞不下），因此read line還是挺常用的
* https://motion-express.com/blog/20150402-basic-file-manipulation-in-ruby

### 關於字串操作

* 如果一次讀了整個檔案，要以換行字元切割開來，該怎麼做呢？ [split](https://ruby-doc.org/core-2.2.0/String.html#method-i-split) 會是個好主意
* http://emn178.pixnet.net/blog/post/110782417-ruby%E6%95%99%E5%AD%B8---%E5%AD%97%E4%B8%B2%28string%29
* https://guides.ruby.tw/ruby/strings.html

### 關於指令行（Command Line Interface - CLI）

* 雖然絕大多數人<strike>被Windows慣壞</strike> 不熟悉命令行操作，但這真的是一大神器，一個資訊人可以不會寫程式，但絕對不能不會指令。 [Linux指令入門](http://linux.vbird.org/linux_basic/0320bash.php)
* 多數指令允許你輸入多個“參數”來控制程式的行為，例如 ```tail /etc/passwd``` 命令代表印出檔案最後10行， ```tail -n 3 /etc/passwd```代表我只要3行。學會使用參數，不再需要你問使用者之後等待輸入，而是程式一啟動東西就都準備好了，多好！
* https://www.codecademy.com/articles/ruby-command-line-argv

### 關於字串轉換

* 有些時候，使用者會輸入一些亂七八糟的東西，搗亂你的美好心情。例如你檔案儲存明明就逗號分格，她偏要輸入逗號; 你檔案用換行字元分格，結果使用者就塞了一篇百行的文章，你的換行又亂掉了。
* 又或者，你得用email當欄位id, 但是HTML表單傳輸時"@"的特殊符號跑出來攪局，傳送不出去，怎麼辦呢？
* [base64 Encoding](https://zh.wikipedia.org/zh-tw/Base64): 最早用在Email系統中，把特殊字元的字串通通轉換成常見字元，等信送到使用者手上再轉回來，就不用怕信件內容一堆有的沒的怪狀況了
* [URLEncoding](https://zh.wikipedia.org/wiki/%E7%99%BE%E5%88%86%E5%8F%B7%E7%BC%96%E7%A0%81): 也是類似的目的，不過專門用在HTML的URL上面，先encode過把URL會用到的特殊符號轉換掉，送到Server再轉回來
* 當然，為了把這些特殊字元重新編碼過，整個文字當然會變得更長，這是他的缺點
* [Online Base64](https://www.base64decode.org/)
* [Online URLEncode](https://www.url-encode-decode.com/)


### 關於Hash與密碼儲存

* 上面提過了encoding，但越邊越長挺浪費頻寬的，而有些時候我們並不在意他能不能轉換回原狀 - 只是要確定東西是對的就好，所以出現了hash。hash是一個不可逆的轉換。不管原文有多長，他都會把它編碼成一串固定長度的字串，而只要原文有任何修改 - 哪怕只是某個大寫變小寫，產生出來的字串都會天差地別。
* 因為這個特性，所以hash很常用在做檢查上。例如我寄一個檔案給你，我怕傳輸壞掉了或有人改過他，我就附上了這個檔案的MD5 hash, 收到的人只要把檔案丟去MD5跑一下，馬上就知道他是不是跟原本的一樣了。
* 也因此，Hash很常用在密碼的處理上。如果我們把使用者的密碼用原本的方式儲存起來，雖然比對很方便，但如果網站被駭客打爆了，大家的密碼就一起噴光光，你知道很多人同一組密碼會用在很多網站上，使用者就倒大楣了。但如果我只儲存密碼的hash, 使用者下次輸入密碼的時候我再hash一下就知道密碼一不一樣，而只儲存密碼hash駭客拿到也“比較”沒辦法知道原本的密碼
* 你應該注意到我上面那句“比較”了...密碼加鹽（slated）、彩虹表與hash碰撞等安全議題，有空再聊 :p
* [MD5 wiki](https://zh.wikipedia.org/zh-tw/MD5)
* [SHA wiki](https://zh.wikipedia.org/wiki/SHA%E5%AE%B6%E6%97%8F)
* [Online MD5](https://www.md5online.org/md5-encrypt.html)
* [Online SHA1](http://www.sha1-online.com/)

### 關於HTML表單

* Lv2 HTTP Server/Client架構 講到，網站事實上就是使用者一次次發送Request給Server, Server處理之後回應串起來的動作，而我怎麼指定傳送資訊給Server, 靠的就是表單。
* 表單由一個form標籤包起來的一組input/select/textarea標籤組合而成，form標籤定義了 這組數據要送到哪、該用GET/POST還是甚麼方法送出，而內部的標籤則定義了要傳送的數據，input/select/textarea標籤的name屬性決定了數據的名稱，而input/select/textarea的內文決定了送出什麼數據。
* 例如 ```<form action="/new_post" method="post"> <input type="text" name="nickname" value="newbie" /><input type="submit" value="送出" /> </form>``` 這一串表示了一個輸入框與按鈕，直接按下送出鈕，數據「nickname=newbie」就會通過post方法送到/new_post這個網址去
* Server（也就是你寫的RoR專案）收到的時候，教學都是教你用form_tag這個輔助功能來處理，你可以直接同時定義表單要有哪些元素，以及數據回來時自動幫你塞到對應的變數之中。
  * https://rails.ruby.tw/form_helpers.html
* 但有些時候這樣並不足夠。如果你遇到“欄位名稱不固定”，或如checkbox這種“你要的數據不在value，而是name本身”的情況，form_tag就不適合了，這個時候就要回到老派一點的做法：直接去讀取Request中攜帶的數據。Rails幫你把所有使用者傳回的參數都放在params這個變數中，你可以利用這個變數取得使用者原始輸入的內容，包含列表他傳送來的所有陣列資訊
  * https://stackoverflow.com/questions/2890069/get-data-from-html-form-to-ruby-in-ruby-on-rails
  * [把陣列中所有元素倒出來](https://stackoverflow.com/questions/310634/what-is-the-right-way-to-iterate-through-an-array-in-ruby)