Challenge Lv0
=====
## 任務目標

* 擁有一個Github帳號，這裡會是你公開程式碼與成果的地方
  * <https://github.com/>
  * <http://blog.kevinlinul.idv.tw/?p=369>
  * **檢查點：請把你的Github帳號的網址傳給我**
* 登入練習機（Linux Ubuntu 16.04）
  * 練習機資訊我已經個別私訊給各位
  * **檢查點：請把你第一次登入成功的畫面截圖給我**
* 認識環境：編輯器
  * 安裝[sublime text 3](https://www.sublimetext.com/3)
  * [sublime text 3課程](https://www.udemy.com/sublime-text-3/)
  * 或你可以[選擇別的](http://rubyer.me/blog/84/)如 [Notepad++](https://notepad-plus-plus.org/zh/) / [Rubymine](https://www.jetbrains.com/ruby/) / [NetBeans](https://netbeans.org/) / [Eclipse](https://www.eclipse.org/) / [Aptana Studio](http://www.aptana.com/) 甚至筆記本，教學自己Google
  * [外掛模組也裝一下](https://blog.miniasp.com/post/2014/01/06/Useful-tool-Sublime-Text-3-Quick-Start.aspx)
  * **檢查點：請把編輯器打開的畫面截圖給我**
* 排定唸書的時間
  * 一週至少四小時實體讀書會，分享學習心得
  * 一週唸書的時間至少8hr
  * 請主動於群組回報並敲定時間
  * **檢查點：請個別回報讀書規劃給我**

## Tips

### 關於Github

* Github是一個讓大家放自己的專案的地方，給大家看一下我的 <https://github.com/sakura26>
  * 首頁以可以看到我做了哪些專案，你可以看到我有哪些專案是大家有興趣的。特別的地方是，你可以看到有星星跟分岔的符號後面跟著數字，星星代表有多少人喜歡你的專案，而分岔代表有人覺得這份專案很棒，建立了一份分枝來改成自己的版本
  * 而下方則是我在這一年內的所有活動，例如修改程式碼、提供貢獻給其他專案等等，高活躍度的人很容易就看得出來
* 至於一個常見的專案長什麼樣？這是我在Github上的第一個專案，[自爆按鈕（？）](https://github.com/sakura26/killallbtn)
  * 在上方有一個狀態列，紀錄了這個專案經歷了六次修改（commits），一個分支（branch），一個開發者（contributor），以及使用哪一種授權公開（這邊用的是BSD授權）
  * 檔案右邊你可以看到最後修改時間、最後修改的意見、點進檔案就可以看到內容
* 他不只可以用來公開你的專案原始碼，我也常常把它拿來當blog寫 [我的釀酒部落格](https://github.com/sakura26/ethanol)
  * 既然要把他當blog寫，總是會想貼點圖或寫得文情並茂一點，這個時候請參考這邊
Github支援顯示的語法有好幾種，但最主要也最好用的叫做Markdown
[語法](https://guides.github.com/features/mastering-markdown/)
  * Markdown的副檔名是 .md 
他是一種，就算你沒有專屬編輯器，打開檔案看起來也會很舒服的一種檔案格式
例如這是我[8/6的釀酒紀錄](https://github.com/sakura26/ethanol/blob/master/brewingHistory/180806-ethen-belgianpaleale.md
)，[原始碼長這樣](https://raw.githubusercontent.com/sakura26/ethanol/master/brewingHistory/180806-ethen-belgianpaleale.md)
  * MD的設計概念就是文字為本體，用人看得懂的方式略為修飾就好。也有線上編輯器，可以一邊打就直接看到出來的結果長怎樣。例如這是我正在學[GoLang的筆記](https://hackmd.io/5RTwaiTSSNqblbNSTqvxmA?both)
* 同時你也可以用它架設你的網站（只限靜態頁面），因此很適合作為純前端展示之用。這是我幫TDOH做的技能樹的網站，實際上就是由Github提供服務的 [駭客學習地圖](http://map.tdohacker.org/) ＝ [原始碼](https://github.com/tdoh/map) 

雖然Git的東西好像很多，不過一般來說你只會用到五個命令而已

* 第一次把專案複製下來的 git clone
* 看系統狀態的 git status
* 把新增或修改的檔案加進去 git add -A
* 確認修改做一次提交 git commit -m "your comments"
* 把程式碼送到遠端同步 git push

只有在多人的情況下，你可能會用到 fetch, pull, checkout, merge等等的，到時候再查吧

### 關於vi / vim

* Linux上預設的編輯器是vi, 自然也是git的預設編輯器。雖然他很不直覺，不過跟Git一樣，我們一般只會用到幾個命令
* 切換指令與編輯模式：一般來說vi就是兩個模式，剛進去的時候是指令。指令模式允許你做一些操作，就像在程式的功能表中一樣，編輯則是在檔案內容中遊走編修。從指令模式切換到編輯模式按i，從編輯模式脫離按ESC。如果你不確定你在什麼模式，就多按幾下ESC吧 
* 在指令模式下，
  * 存檔是 :w
  * 存檔同時退出vi :wq
  * 不要存檔退出 :q!
  * 搜尋字串abc /abc
* 還有很多快速鍵幫你加速操作，不過一般來說你記住這幾個就夠了

### 關於第一次登入Linux主機

* 請使用ssh連線上去，他沒有視窗沒有桌面，完全是指令行
* 登入的方式請參考[這篇](https://ph302.cs.pu.edu.tw/putty.htm)
* 請從這邊下載[putty](https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe)

![](img/lv0_1.png)

* 這個畫面代表你成功登入了這台主機，這是這台主機給你的歡迎畫面，一些簡介，而最後一行代表機器在等待你輸入指令
* <你的帳號>@<這台主機名稱>:<你現在的目錄>$ 
* 你現在的身份是一般使用者，所以結尾是$，如果是特權帳號，結尾則是#
* 以這個例子來說，帳號是sukekiyo166，主機名稱是newgamesukekiyo166，你現在的目錄是~，代表你的家目錄的縮寫，實際上完整路徑是 /home/sukekiyo166
* 你現在只需要確認你可以連上去就好，接下來開始學linux基礎的時候，所有的練習都在這上面進行，同時接下來學RoR的時候，架設伺服器也會使用這一台。
* 你可以任意使用它，搞壞了跟我說，我幫你做系統還原（不過所有你在上面的資料也都會消失）
