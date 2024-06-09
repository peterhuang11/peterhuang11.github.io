# Day9 伺服器環境規畫建置

+ 基本指令
    + mkdir 建立一個空目錄
    + cp 複製目錄
    + rm 刪除目錄
    + 2> /dev/null 錯誤資料導向垃圾桶

+ 檔案管理指令
    ||檔案|目錄|
    |--|--|--|
    |新增|touch, vim, nano|mkdir|
    |修改|cp, mu|cp -r,cp -a, mu, cd|
    |刪除|rm|rmdir, rm -rf|
    |查詢|find, locate, pwd, ll, ls|find, locate, pwd, ll, ls|

+ 萬用字元
    |符號|說明|
    |-|-|
    |* |代表任意字元
    |?|代表一個任字字元
    |[]|代表存在括號中字元中的任一個字元
    |[-]|代表為括號中之編碼連續的任一個字元
    |^|為反向選擇，即不存在包括^表示的任一個字元
:::info
例題 3.1.1-1：了解基礎的工作目錄切換、觀察隱藏檔、複製檔案、刪除非空白目錄等任務。請以 student 身份完成下列動作。
1. 前往 /dev/shm 目錄
    ==cd /dev/shm==
2. 在該目錄下建立名為 class3 的子目錄
    ==mkdir class3==
3. 觀察 /dev/shm/class3 這個目錄的內容，並請說明內部有沒有其他檔案 (註：使用 ll 加上顯示隱藏檔的選項)
    ==class3為空目錄；顯示隱藏檔ll指令加 -a 參數==
4. 透過 cp /etc/hosts /dev/shm/class3 將檔案複製到該目錄內，並觀察 class3 目錄的內容
    ==class3目錄多了一個名為hosts的檔案==
5. 使用 rmdir /dev/shm/class3 嘗試刪除該目錄，並說明可以或不行刪除該目錄的原因
    ==rmdir 為刪除空目錄指令，需將目錄中檔案刪除才可使用==
:::

:::info
例題 3.1.1-2：讓含有資料的目錄變成空目錄，再以 rmdir 刪除
1. 承上一個例題，進入到 /dev/shm/class3 當中，並且使用 rm 刪除掉所有該目錄下的檔案 (非隱藏檔)
    ==cd /dev/shm/class3==
    ==rm hosts==
2. 回到 /dev/shm 當中，此時能否使用 rmdir 刪除 class3 目錄？為什麼？
    ==可以刪除class3，此時該目錄為空目錄，可使用rmdir指令刪除==
:::

:::info
例題 3.1.2-1：使用萬用字元搭配，來找出某些特殊的檔名
1. 列出 /etc/ 底下含有 5 個字元的檔名
    ==ls /etc/???\??==
3. 列出 /etc/ 底下含有數字在內的檔名
    ==ls /etc/*[0-9]\*==
:::

+ 檔案及目錄的複製與刪除
    + 複製使用 cp 指令，若需要複製目錄，參數一般使用 -r，需要完整備份，參數使用 -a (可完整複製該檔權限及檔案時間)
    + 刪除使用 rm、rmdir(刪除空目錄) 指令，
    + 建立或刪除目錄或檔案名稱含有空白字元，可使用單引號、雙引號或\進行處理。
    + 建立或刪除目錄或檔案名稱含有+或-字元，前方需加上絕對路徑或相對路徑
    + ll -a 顯示隱藏檔及一般檔案(以小數點開頭檔名為隱藏檔)
    + ll -d .*　僅顯示隱藏檔
    + file 查詢檔案類型與型態 

:::info
例題 3.1.3-1：目的地的目錄是否存在，會影響到複製的行為。
1. 先進入 /dev/shm ，同時觀察目錄下有無名為 rc.d 的檔名
    ==cd /dev/shm==
    ==ll /dev/shm/rc.d==
    ==查無該檔案==
2. 使用『 cp -r /etc/rc.d rc.d 』將 rc.d 複製到本目錄下，然後使用 ll 與 ll rc.d 觀察該目錄
    ==ll 查詢shm目錄中是否有rc.d目錄==
    ==ll rc.d 查詢該目錄中的檔案==
3. 重新執行上述複製的指令一次，然後使用 ll rc.d ，觀察一下有什麼變化？
    ==rc.d目錄中又新增一個rc.d的目錄==
:::

:::info
例題 3.1.3-2：刪除的實驗
1. 進入 /dev/shm ，觀察到前一個例題 /dev/shm/rc.d 的目錄存在後，請將它刪除
    ==cd /dev/shm==
    ==rm -rf rc.d==
:::

+ 檔名移動與更名
  + mv 指令用於搬移檔案或更改檔案名稱 
    
:::info
例題 3.1.6-1：如何進行檔案的更名
1. 讓 student 回到家目錄
    ==cd ~==
3. 將 /etc/rpm 複製到本目錄
4.  ==cp /etc/rpm .==
5. 該目錄移動錯誤，請將本目錄的 rpm 移動到 /dev/shm
    ==mv rpm /dev/shm==
7. 檔名依舊錯誤，請將 /dev/shm 底下的 rpm 更名為 mail3
    ==cd /dev/shm/
    ==mv rpm mail3==
:::

:::info
例題 3.1.7-1：大量建置檔案的方法，透過 {} 的輔助
1. 我需要在 /dev/shm/testing 目錄下建立名為 mytest_XX_YY_ZZ 的檔案，其中 XX 為 jan, feb, mar, apr 四個資料， YY 為 one, two, three 三個資料，而 ZZ 為 a1, b1, c1 三個資料，如何使用一個指令就建立出上述的 36 個檔案？
    ==mkdir testing==
    ==cd testing==
    ==touch mytest_{jan,feb,mar,apr}\_{one,two,three}_{a1,b1,c1}==
2. 我需要在 /dev/shm/student/ 目錄下，建立檔名為 4XXXC001 到 4XXXC050 的檔案，如何使用一個指令來完成這 50 個檔案的建置？
    ==mkdir student==
    ==touch 4XXXC{001..050}==
:::

+ 新增檔案
    + touch 指令，可用{}建立多個名稱檔案

+ 查詢檔案內容
    + cat 顯示檔案全部內容
    + head 僅顯示前10行內容
    + tail 僅顯示最後10行內容
    + 可使用 -n 參數加上預查看的行數數值；例 head -n 5 /etc/passwd 顯示passwd檔案前5行內容

:::info
例題 3.2.2-1：了解 more 與 less 的用法
1. 使用 more /etc/services 一頁一頁翻動資料
2. 承上，請找出 http 這個關鍵字，之後直接離開不再查閱
3. 使用 less /etc/services 查詢檔案內容
4. 承上，請找出 http 這個關鍵字，重複查詢 http 數次後，之後直接離開不再查閱
:::


+ vim程式編輯器
    + 一般指令模式：使用「vim filename」進入 vim 之後，最先接觸到的模式。模式下可以進行複製、刪除、貼上、移動游標、復原等任務。
    + 編輯模式：在一般指令模式底下輸入「i」這個按鈕，進入編輯模式，可以開始打字編輯文件。
    + 延伸指令列命令模式：此模式可以進行儲存、離開、強制離開、搜尋、取代。
    + 選取模式：此模式進行類似滑鼠圈選的選取模式，主要分為三種圈選方式：
        + v ：字元方式圈選；
        + [shift]+v ：以整行方式圈選
        + [ctrl]+v ：以區塊方式圈選
            圈選完畢後，可以按 y 複製、按 d 刪除，在其他地方可以按 p 貼上

+ |慣用的指令|	說明
    |-|-|
    |i, [esc]|i 為進入編輯模式，[esc] 為離開編輯模式
    |G	|移動到這個檔案的最後一列
    |gg	|移動到這個檔案的第一列
    |nG	|n 為數字，移動到這個檔案的第 n 列，例如 10G 為讓游標去到第 10 列
    |dd	|dd 為刪除游標所在行，5dd 為刪除 5 行，ndd 為刪除 n 行
    |yy	|yy 為複製游標所在行，5yy 為複製 5 行，nyy 為複製 n 行
    |p	|在游標底下貼上剛剛刪除/複製的資料
    |u	|復原前一個動作
    |:w	|將目前的資料寫入硬碟中
    |:q	|離開 vim
    |:q!|	不儲存 (強制) 離開 vim
    

# 課後練習操作
:::info
+ 關於 vim 建立檔案，以及資料的轉存情況：(使用 student 身份)
1. 先用 vim 建立一個名為 /dev/shm/mycheck.txt 的檔案，裡面填寫你的姓名與學號，一行一個
==vim /dev/shm/mycheck.txt==
    :::danger
    + vim 為檔案編輯器
    + 使用 dd 為刪除游標該行數，前面加數值再按dd為刪除數值之行數
    + 使用 yy 為複製游標該行數，前面加數值再按yy為複製數值之行數，使用p為貼上
    + 使用 u 為回復上一動作
    + 使用 i 進入編輯模式，按Esc鍵退出模式
    + 使用 :wq 退出vim模式；w為存檔、q為離開
    :::
2. 使用 file 去檢查 /etc/group /bin/groups 的檔案類型，並將查詢的資料轉存並累加到 /dev/shm/mycheck.txt 當中
==file /etc/group /bin/groups >> /dev/shm/mycheck.txt==
    :::danger
    + file 指令為查詢檔案類型與型態
    :::
3. 查詢出 /etc/ 底下，使用 s 開頭以及 s 結尾的檔名 (不含子目錄下的檔案)，並將找到的檔名轉存並累加一份到 /dev/shm/mycheck.txt 當中
==ll -d /etc/s*s >> /dev/shm/mycheck.txt==
4. 找出最近有使用過的 rm 的指令，並將該執行的指令轉存並累加到 /dev/shm/mycheck.txt 當中
==history | grep rm >> /dev/shm/mycheck.txt==
    :::danger
    + 使用 history 查詢歷史指令，再使用 | 管線與查詢關鍵字 grep 指令，再轉存至 mycheck.txt 
    :::
5. 將 /etc/passwd 前 5 行與最後 5 行抓出來，並且附上行號之後，轉存並累加到 /dev/shm/mycheck.txt 當中
==head -n 5 /etc/passwd >> /dev/shm/h5.txt==
==tail -n 5 /etc/passwd >> /dev/shm/t5.txt==
==cat -n /dev/shm/h5.txt /dev/shm/t5.txt >> /dev/shm/mycheck.txt==
    :::danger
    + 第一步先使用head -n 5 取前5行，並暫存至h5.txt
    + 第二步使用tail -n 5 取最後5行，同樣存至t5.txt
    + 第三步使用cat 指令顯示檔案全部內容再使用-n參數每行加上編號，轉存至 mycheck.txt中
    :::

+ 關於檔案管理：(使用 student 身份)
1. 嘗試在 /dev/shm/unit03/files/ 目錄下，新增 ksu001 ~ ksu100 這 100 個空檔案
==mkdir -p /dev/shm/unit03/file/ksu{001..100}==
    :::danger
    + mkdir 指令為新增空目錄，參數-p 為需要時建立目標目錄的上層目錄，即使這些目錄已存在也不當作錯誤處理
    :::
2. 嘗試在 /dev/shm/unit03/dirs/ 目錄下，新增 dir01 ~ dir10 這 10 個空目錄
==mkdir -p /dev/shm/unit03/dirs/dir{01..10}==
3. 嘗試在 /dev/shm/unit03/season/ 目錄下，新增 jan, feb, mar 這三個空目錄
==mkdir -p /dev/shm/unit03/season/{jan,feb,mar}==
4. 嘗試在 /dev/shm/unit03/seaon/ 目錄下的 jan, feb, mar 子目錄內，建立 mylog_XX_YY_ZZ.txt 空檔案，其中：『XX 為 1~9』, 『YY 為 aa 與 bb』，『ZZ 為 start 與 end』。
==touch /dev/shm/unit03/season/{jan,feb,mar}/ mylog_{1..9}_{aa,bb}\_{start,end}.txt==
5. 嘗試在 /dev/shm/unit03/spc/ 目錄下，建立名為 -check.txt 的目錄
==mkdir -p /dev/shm/unit03/spc/-check.txt==
    :::danger
   + 新增有+或-符號檔名時，需加上相對路徑或絕對路徑
:::