# picoCTF
<font size='5px' color='#FF1493' face="DFKai-sb"><b>

</b>
</font>
## <font size='10px'>Web Exploitation</font>
### <font size='6px'>題目GET aHEAD</font>
![](https://i.imgur.com/gWuXnHM.png)
* <font color='red'>提示</font>
    1. 他說可能我們用大於兩種的選擇
    2. 我們可以透過burpsuit類似工具來修改請求
* <font color='red'>解題思路</font>
    先打開F12看一下，我們會看到html裡面兩個按鈕請求不一樣。
    ![](https://i.imgur.com/FgXxGhS.png)
    一個是GET 跟POST當然根據提示我們還可以用別種請求試試看，
    這裡用到[curl指令](https://blog.techbridge.cc/2019/02/01/linux-curl-command-tutorial/)
    ```bash
    $curl -I URL
    ```
    就會顯示出來了
    ![](https://i.imgur.com/fsy8y7v.png)

### <font size='6px'>題目Cookies</font>

![](https://i.imgur.com/H58sjM3.png)
* <font color='red'>解題思路</font>

    看題目一定八九不離十跟cookie有關係，
    一樣打開F12->application 改改看cookie，
    會發現每改一次他輸出都不太一樣，可以順著這個思路去改改看，
    會發現在name=18時，可以看到我們的flag。
    
    不過這題是因為數字比較小，如果牠放到很後面，我們當然不可能慢慢點，
    所以我們可以通過寫程式方式，我這邊提供[別人的程式](https://github.com/JeffersonDing/CTF/blob/master/pico_CTF_2021/web/cookies/ape.py)，他用py迴圈去檢測，當然也可以直接在shell下 
    ```bash
    $for i in {1..100}; do #你要的指令curl之類的
    ```
### <font size='6px'>題目Insp3ct0r</font>
![](https://i.imgur.com/xos4X4E.png)
* <font color='red'>解題思路</font>
    題目說了要我們檢查code，我們就F12檢查吧，
    首先看到html他有註解沒有刪掉，而且看起來像旗幟
    ![](https://i.imgur.com/TSR4lOj.png)
    不過好像只給1/3的部分，我們接著找其他檔案。
    F12->Source 依序在js 跟css找到我們剩餘的flag。
    這題對新手蠻實用的，許多人架網站註解都會忘記刪掉。
    
### <font size='6px'>題目Scavenger Hunt</font>
![](https://i.imgur.com/Z3hvf4a.png)
* <font color='red'>解題思路</font>
    題目叫做尋寶獵人，且敘述說周圍隱藏者一些有趣的訊息，
    感覺就跟上一題很像，那我們一樣檢查網站的code，馬上就在html看到一小段flag，
    css第二段，可惜的是js沒有找到但他也提供我們訊息防止google引擎查詢，
    馬上就聯想到[robots.txt](https://www.newscan.com.tw/all-seo/robots-block-search-engines.htm)，我們訪問看看。
    ![](https://i.imgur.com/5sbYgRV.png)
    這裡也出現一段flag並出現提示，網頁適用阿帕契架的，那就有可能會有[.htaccess](https://www.newscan.com.tw/all-seo/block-search-engines-htaccess.htm)，我們在這裡找到第四段，接下來的提示是mac，那我們再找找看[.DS_Store](https://zh.wikipedia.org/zh-tw/.DS_Store)全部flag就找到了。
    
### <font size='6px'>題目where are the robots</font>
![](https://i.imgur.com/HghEyZa.png)
* <font color='red'>解題思路</font>
    題目寫哪裡有robots，還記得上一題我們才剛剛寫到robots.txt嗎，
    我們試試看直接去查看/robot.txt，發現他有阻止一個網站被找到，
    ![](https://i.imgur.com/yqFjquq.png)
    我們就去看看這是甚麼網站吧，很好進去答案就找到了:>

### <font size='6px'>題目logon</font>
![](https://i.imgur.com/plk8Aq4.png)
* <font color='red'>解題思路</font>
    題目說好像不會講檢查登入?除了joe，那我們猜測joe應該是root管理員，
    我先隨便打帳密進去，進去發現應該是權限不足? !，F12到處檢查一下，
    我發現cookie有一個admin=false看起來超奇怪的，我把它改成True，
    結果Flag就出來了
    
### <font size='6px'>題目dont-use-client-side</font>
![](https://i.imgur.com/z5epn6a.png)
* <font color='red'>解題思路</font>
    題目說沒有使用者? !不太懂他得意思，
    沒關係我們一樣F12看一下有沒有可以利用的咚咚，
    我看了一下Html裡面藏著js驗證指令
    ![](https://i.imgur.com/jP94WrL.png)
    細看發現，把後面按照split順序拼起來就是flag，
    <font color='	DeepPink'>picoCTF{no_clients_plz_7723ce}</font>
    我也懂了為啥叫做沒有使用者，因為他怎麼樣都不會進去。
    你正確他也不會跳轉，他只會跟你講對了而已。

### <font size='6px'>題目login</font>
![](https://i.imgur.com/UPc3LDI.png)
* <font color='red'>解題思路</font>
    打開F12，東看看西看看看到他的js，感覺很奇怪我們可以用[縮排網站](https://www.tutorialspoint.com/online_javascript_formatter.htm)幫忙縮排，
    然後縮完，會看到一串很像base64的密文
    ![](https://i.imgur.com/uAWw6C5.png)
，可以用線上[Decode解解看](https://emn178.github.io/online-tools/base64_decode.html)答案就出來了。

### <font size='6px'>題目Includes</font>
![](https://i.imgur.com/KbeYMm3.png)
* <font color='red'>解題思路</font>
    這題我是不太知道要考甚麼，他說去維基百科查include，好吧，
    一樣先看F12有啥東西，恩..js跟css註解就有答案了，完全不知道這題要考啥。

### <font size='6px'>題目Inspect HTML</font>
![](https://i.imgur.com/KhGDjbJ.png)
* <font color='red'>解題思路</font>
    題目叫做檢查html，那就F12一樣檢查看看吧，恩..又是註解。
    你看超簡單你只要會看F12就能解大部分題目了。

### <font size='6px'>題目Local Authority</font>
![](https://i.imgur.com/k9Iz5eD.png)
* <font color='red'>解題思路</font>
    看到題目這個名字，我以為是改cookie之類的，因為我點開也有admin咚咚，
    超奇怪但我試了幾次都沒有，我點開了提示，他說檢查看看網站是怎麼驗證的，
    那我們就登登看，發現會跳轉到login.php，我們打開看一下F12，
    他驗證的程式有沒有寫在裡面吧，欸發現了secure.js點開就會看到帳密，
    登進去flag就出來了。


### <font size='6px'>題目Search source</font>
![](https://i.imgur.com/uCBGBHO.png)
* <font color='red'>解題思路</font>
    題目說好像有留強大重大的神器?，不太懂不管我們一樣F12找找看，
    他的網站超級多的，為了效率我們ctrl+f搜尋picoCTF，結果發現在style.css，
    裡面出現flag。
### <font size='6px'>題目caas</font>
![](https://i.imgur.com/fiZoP7e.png)
* <font color='red'>解題思路</font>
    這題還蠻有趣的，點開網站看得出，他叫我們把訊息寫在網址後，
    就能跟這個cowsay互動，不管寫甚麼他都可以印出來，那我們試試看有沒有文件漏洞，
    我打上linux指令，盡然可以互動欸
    ![](https://i.imgur.com/TnRfj9j.png)
    那我們查查看這個falg.txt看起來超奇怪的檔案，
    在後面加cat falg.txt答案就出來了。
    ![](https://i.imgur.com/NCrbNhg.png)
    這個題目超有趣
### <font size='6px'>題目picobrowser</font>
![](https://i.imgur.com/TmOXYCq.png)
* <font color='red'>解題思路</font>
    這題我點網址進去，中間出現了flag看起來很奇怪，點點看，
    跳出了
    ```
    You're not picobrowser! 
    Mozilla/5.0 (Windows NT 10.0; Win64; x64)
    AppleWebKit/537.36 (KHTML, like Gecko) 
    Chrome/108.0.0.0 Safari/537.36
    ```
    反正就是要我用picobrowser才給我點，F12的右邊點更多，有一個
    more tool然後裡面有一個network conditions，點開可以改瀏覽器名字
    我們可以把它改成他要的picobrowser像這樣
    ![](https://i.imgur.com/5PfqYqA.png)
    重新點就可以了，flag就出來了
### <font size='6px'>題目Client-side-again</font>
![](https://i.imgur.com/wMMH3RS.png)
* <font color='red'>解題思路</font>
    他說我們能不能闖進這個超強門呢，恩不知道一樣F12打開，
    欸奇怪盡然沒有js或是css檔案，不過他要驗證一定會有js，所以應該是寫在
    html裡面，我們看一下，果然有一個很長的js code，我們複製用之前那個
    [js排版工具](https://www.tutorialspoint.com/online_javascript_formatter.htm)
    我們會看到一堆flag片段，我們按造順序把它組合起來就是答案了。
    不過組合過程偏麻煩，還要用到F12 console查看js變數，然後一個一個對照，
    我這裡就不做了，我傳別人寫好的[網址](https://ithelp.ithome.com.tw/articles/10246749)

### <font size='6px'>題目Web Gauntlet</font>
![](https://i.imgur.com/a9OfGvi.png)
* <font color='red'>解題思路</font>
    這題看提示似乎要我們用注入器，但是可能給我們另一個網址好像是他的過濾器，
    我們可以對應看看過濾器，下面是每個回合。
    1. 第一回合過濾器說不能用OR，那我們試試看admin' --
    2. 第二回合過濾器說不能用--，那我們用admin'/*
    3. 第三回合過濾器說不能用><，那等於上回合還可以用
    4. 第四回合過濾器說不能用admin，那我用字串結合的方式a'||'dmin'/*
    5. 第五回合過濾器說不能用union攻擊，那上回合一樣可以用
    最後他叫我們再去檢查看看filter.php，裡面就出現了全部回合的驗證步驟，
    以及flag註解，這題可以上網查sql注入清單一個一個是拉。
        
    


### <font size='6px'>題目Irish-Name-Repo 1</font>
![](https://i.imgur.com/4nXEwH1.png)

* <font color='red'>提示</font>
    1. 我想知道用戶是否保存在數據庫中？
    2. 嘗試考慮網站如何驗證您的登錄信息。

* <font color='red'>解題思路</font>

    從以上提示能判斷出，題目想要叫我們去看他的程式碼是怎麼判別登入的。
    首先F12 Elements 層層打開能看到一個login.php 用post
    
    ![](https://i.imgur.com/Uo47ufZ.png)
    
    我們試試看把debug 後面value改成1
    ![](https://i.imgur.com/64wOo3P.png)
    跳出這個sql的語法，那我就能試試看以前sql注入的漏洞
    參考網址:https://ithelp.ithome.com.tw/articles/10189201
    
    在username上打'OR 1=1 -- 便能破解
    ![](https://i.imgur.com/dr23RCw.png)
### <font size='6px'>題目Forbidden Paths</font>

![](https://i.imgur.com/DXRdObo.png)
* <font color='red'>解題思路</font>
    題目說flag在flag.txt上
    進到網頁我們會發現這個read看起來很可疑
    ![](https://i.imgur.com/RJyhu1T.png)
    又因為題目說nginx的index放在/usr/share/nginx/html下
    所以我用打了linex語法 ../../../../flag.txt
    便找到
![](https://i.imgur.com/yU5hXld.png)

### <font size='6px'>題目SQLiLite</font>

![](https://i.imgur.com/dLjoYlV.png)
* <font color='red'>解題思路</font>
     測試了一下發現也是sql注入
     一樣打'OR 1=1 -- 就可以登入
     當然他的flag藏起來了，這裡F12打開就可以看到
     ![](https://i.imgur.com/q32GJuq.png)
## <font size='10px'>Foriensics 鑑識</font>
 
 <font color='purple' size='6px'><span>基本工具</span> </font>
 * binwalk
 * [strings](https://eecsmt.com/linux/linux-strings/)
 ### <font size='6px'>題目Matryoshka doll </font>
 
 ![](https://i.imgur.com/YKl9YZV.png)
  * <font color='red'>解題思路</font>
     提示中跟我們講，有隱藏的文件那我們用binwalk掃掃看
     ```bash
     $binwalk -e dolls.jpg
     ```
     會發現隱藏文件出來了
     一層一層的解開會找到最後一層的flag.txt
 ### <font size='6px'>題目Glory of the Garden</font>
 
![](https://i.imgur.com/07N01LC.png)
 *  <font color='red'>解題思路</font> 
     直接點開裡面的圖長這樣
     ![](https://i.imgur.com/PO8gt1V.jpg)
     提示有說16禁制編輯器?
     我們先用vim打開看看，然後<font color='pink'>/picoCTf</font>就出現了，
     他藏在最後面
     ![](https://i.imgur.com/cH9EoIM.png)
 

 ### <font size='6px'>題目Enhance!</font>
 
 ![](https://i.imgur.com/VsfUMtq.png)

* <font color='red'>解題思路</font>
     strings指令用來檢視二進位檔案。
     用strings來檢查看看
     會發現答案藏在裡面
    ```bash
    $strings drawing.flag.svg
    ```
 ### <font size='6px'>題目Lookey here</font>
 
 ![](https://i.imgur.com/Ytk0J7E.png)
 
* <font color='red'>解題思路</font>
     需要了解grep用法 
     ．*代表所有字元都可替代
    ```bash
    $cat anthem.flag.txt | grep picoCTF{.*}
    ```

### <font size='6px'>題目Packets Primer</font>

![](https://i.imgur.com/1UtgW9q.png)

* <font color='red'>解題思路</font>
    用wireshark打開選擇任一個tcp
    右鍵點擊follow看他的tcp stream裡面就是我們找的flag

### <font size='6px'>題目Redaction gone wrong</font>

![](https://i.imgur.com/B13Ywjp.png)

* <font color='red'>解題思路</font>
    把下載完的pdf點開，發現有一部分是黑的
    ![](https://i.imgur.com/ETJfJoZ.png)
    我們試試將他反白就會發現最後一個是我們的flag

### <font size='6px'>題目So Meta</font>

![](https://i.imgur.com/dvMVJR1.png)

* <font color='red'>解題思路</font>
     二進制打開順便記得用grep查查看
    ```bash
    $strings pico_img.png | grep picoCTF{.*}
    ```
    可以找到我們的flag了
    
    
### <font size='6px'>題目shark on wire 1</font>

![](https://i.imgur.com/JLriV5c.png)

* <font color='red'>解題思路</font>
    提示要我們用wireshark以及檢查所有stream
    我們就一個一個檢查，檢查到第六個時找到了答案
    ![](https://i.imgur.com/TmCJGfb.png)
    
### <font size='6px'>題目extensions</font>

![](https://i.imgur.com/xfmzq9o.png)

* <font color='red'>解題思路</font>
    我們vim打開發現一堆亂碼，但開頭顯示png
    代表這有可能是一個png檔，我們將他改副檔名
    便成功找出flag

### <font size='6px'>題目What Lies Within</font>

![](https://i.imgur.com/FheIBKQ.png)

* <font color='red'>解題思路</font>
    提示叫我們找線上decode，那我們就找吧
    找[decode image](https://stylesuxx.github.io/steganography/)
    照片上傳上去flag就出來了

### <font size='6px'>題目MacroHard WeakEdge</font>

![](https://i.imgur.com/5bCz9iB.png)

* <font color='red'>解題思路</font>
    這題好難好麻煩，我看這個人的[解答](https://ctftime.org/writeup/26975)
    我列出幾點我比較不熟習
    1.     $7z -x file(解壓縮)
    2.     ls -la *(可以遞迴顯示)
    3.     echo "string" | base64 -d (解密)
    依序上面三點網址
    [7z](http://note.drx.tw/2008/04/command.html)
    [ls *](https://n.sfs.tw/mymedia/index/10365)
    [base64](https://shengyu7697.github.io/linux-base64/)

## <font size='10px'>General Skills</font>
[**grep指令**](https://blog.gtwang.org/linux/linux-grep-command-tutorial-examples/)
```bash
$grep 關鍵字 檔案1 檔案2 ...
$grep 關鍵字 /kali/123.file
$grep 關鍵字 /kali/*.conf #在kali下所有.conf，尋找關鍵字
$grep -i 關鍵字 /kali/123.file #不分大小寫
$grep -n 關鍵字 /kali/123.file #顯示行數
$grep -v 關鍵字 /kali/123.file #反向搜尋除了關鍵字其他顯示
$grep -r 關鍵字 /kali/123.file #遞迴搜尋
$grep -A 1 關鍵字 /kali/123.file #多顯示後一行
$grep -B 1 關鍵字 /kali/123.file #多顯示前一行
$grep -B 1 關鍵字 /kali/123.file #多顯示前後各一行
```

[**find指令**](https://blog.gtwang.org/linux/unix-linux-find-command-examples/)

```bash
$find / -name "flag.txt" #從根目錄底下搜尋
$find / -name "flag.txt" 2>/dev/null #過濾掉報錯訊息
```

### <font size='6px'>題目Big Zip</font> 

![](https://i.imgur.com/3dJD3J3.png)
* <font color='red'>解題思路</font>
    這題解壓縮完有許多txt檔跟資料夾
    要從這麼多資料一個一個找到flag
    是有點難，所以要透過grep來尋找
    ```bash
    $unzip  big-zip-files.zip
    $grep -r pico *
    ```
    
### <font size='6px'>題目First Find</font>
![](https://i.imgur.com/bI87fdh.png)
* <font color='red'>解題思路</font>
    此題跟上一題有異曲同工之妙
    解壓縮完看起來很多資料夾跟txt
    我們一樣用grep 遞迴去尋找
    ```bash
    $unzip  files.zip
    $grep -r pico *
    ```

### <font size='6px'>題目Based</font>
![](https://i.imgur.com/ZXMGTnd.png)

* <font color='red'>解題思路</font>
     反正就是nc連線過去會出現一堆題目，
     教你分別把二、八、十六進制轉成string
     我們可以用線上轉換器
     [二進制、十六進制to string](https://www.rapidtables.com/convert/number/binary-to-ascii.html)
     [八進制to string](http://www.unit-conversion.info/texttools/octal/)
     我不知道為啥第一個網站沒辦法八進制轉string
     回答完flag就跑出來了

### <font size='6px'>題目mus1c</font>
![](https://i.imgur.com/qOCPXw1.png)

* <font color='red' >解題思路</font>
     老實說這題我是看不懂要幹嘛，
     但提示有講到rockstar這程式語言
     我們就將他給的文件丟上去看看
     [網站](https://codewithrockstar.com/online)
     
     轉換發現看起來像是ASCII
     我們丟上去ASCII to string的[網站](https://codebeautify.org/ascii-to-text)
     發現出現<font color='blue'>rrrocknrn0113r</font>
     轉成<font color='pink'>picoCTF{rrrocknrn0113r}</font>
     就是答案了
    
### <font size='6px'>題目flag_shop</font>

![](https://i.imgur.com/gKHrvc2.png)

* <font color='red' >解題思路</font>
     這題我們先看他的程式<font color='blue'>store.c</font>
     然後看了一下提示，我猜是要把c程式用爆，
     c的int是有[大小限制的](https://openhome.cc/Gossip/CGossip/Datatype.html)
     我們是看看輸入會超過的範圍，他將會產生亂數使我們金額剩餘超大
     便可以買我們的flag了



