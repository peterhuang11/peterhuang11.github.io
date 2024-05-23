# Day2 伺服器環境規畫建置

## ==教材來源：==
+ 教學網站(鳥哥私房菜)：Linux.vbird.org
+ 教室Vnc連線網址：10.10.53.198:5900 (請開啟RealVNC Viewer程式)
+ CentOS Stream 9 ISO檔 [下載](https://www.centos.org/centos-stream/#tab-3)
+ VMware Workstation Pro[下載](https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware%20Workstation%20Pro)
:::danger
註：下載VM 需要先到 http://support.broadcom.com 註冊帳號
參考來源：https://www.ithome.com.tw/news/162908
:::

## ==虛擬機環境設置==
1. 開啟VMware Workstation Pro
2. Create a New Virtual Machine  新增虛擬機
3. 選擇Typical(recommended)
4. 選擇I will install the operating system later.
   The virtual machine will be created with a blank hard disk.
6. Guest operating system選擇Linux
7. Version 選擇 Red Hat Enterprise Linux 9 64-bit
8. Virtual machine name：虛擬機名稱，自行命名
9. Location：安裝位置，自行指定
10. Specify Disk Capacity 指定磁碟容量
:::info
Maximum disk size(GB)：設定50.0
選擇 Store virtual disk as a single file
:::
10. 點選Customize Hadware 進行硬體參數設定
:::info
Memory 設定為 8 GB
Processors 設定
Number of processos 設定為 1
Number of cores per processor 4
:::
11. 點選 New CD/DVD SATA 選擇右下方 Use ISO image file, 
:::info 
此處請選擇下載存放的CentOS9 ISO檔
:::
12. 回到 New Virtual Machine Wizard 視窗，點選「Finish」

## ==安裝 CentOS9==
1. 點選 Power on this virtual machine 開機
2. 等待讀取ISO檔資料
3. 點選 VM視窗( 此時鼠標會消失，可按 ctrl + alt 鍵切換)
4. 按壓方向鍵選擇 Install CentOS Stream 9 進行安裝
5. 系統語言：可選繁體中文
6. Software Selection：選擇Server with GUI
7. 鍵盤配置：鍵盤佈局, 英文排序設為最上方
8. Language Support：新增英文(美式)
9. Installation Desination：自動選擇
10. KDUMP 關閉
11. 設定Root Password
    1. Lock root account 取消勾選
    2. Allow root SSH login with password 取消勾選
12. 創建使用者，設定帳戶名稱及密碼
13. 完成 Begin Installation
14. 重新啟動電腦，登入系統

## ==備份虛擬機OS==
1. 原OS名稱上方點選右鍵
2. 選擇Manage
3. 選擇Clone
4. 選擇Create a full done
5. 設定名稱、存放路徑

## ==介面說明==
1. 點選「概覽」(瀏覽器．檔案．軟體．求助．終端機．顯示應用程式)
2. 點選「終端機」
    1. 輸入su – root> ==切換root使用者==
    2. 輸入root密碼
    3. yum search ==Chinese ==搜尋中文輸入法==
    4. 選擇要安裝輸入法名稱，例：yum install ibus-table-chinese-array.noarch
    
基本指令
|名稱    |說明                   |
|-------|-----------------------|
|su     |Switch User，用於身份切換 |
|yum    |尋找、安裝、刪除某一個、一組甚至全部軟體包的指令|
|help   |查詢指令說明             |
|history|查詢輸入歷史指令          |
|exit   |離開                    |

:::success
參考來源：[www.runoob.com](https://www.runoob.com/linux/linux-yum.html)
:::

## ==硬體與作業系統介紹==
* 電腦硬體架構：自行查閱教材說明
* linux作業系統發展沿革
    * 重要年份
        * 1969年 C語言
        * 1973年 Unix誕生
        * 1991年 Linux起源
        * 2020年 Linux kernel version 6.0 發佈

## ==例題試作==

:::info
例題 2.1.1-1 使用 date -\-help 找出說明文件，進一步完成底下的動作：
1. 如果需要秀出『 小時:分鐘 』的格式，例如：『 15:20 』，要如何執行指令？
    :::spoiler Ans
        date +"%H:%M"
    :::
2. 請直接輸入指令『 date +%s 』，對照 -\-help 功能，查詢一下輸出的資訊是什麼？
    :::spoiler Ans
        1970-01-01 00:00:00 UTC 以來的秒數
    :::
3. 如果要顯示兩天以前 (2 days ago) 的『 +%Y/%m/%d 』，要如何下達指令？
    :::spoiler Ans
        date -d "-2 days" +%Y/%m/%d
        date -d -2days +%Y/%m/%d
    :::
4. 如果需要顯示出『 西元年-日-月 小時:分鐘 』的格式，日期與時間中間有一個空格！該如何下達指令？
    :::spoiler Ans
        1. date +"%Y-%m-%d %H:%M"
        2. date +%Y-%m-%d\ %H:%M
    :::
:::

:::info
例題 2.1.1-2：使用 cal 搭配 cal -\-help 查詢相關選項，完成底下的題目。
1. cal 這個指令的功能是什麼？
    :::spoiler Ans
       顯示月曆
    :::
2. 顯示目前這個月份的月曆
    :::spoiler Ans
       cal -1
    :::
3. 顯示今年的年曆
    :::spoiler Ans
       cal -y
    :::
4. 顯示前一個月、本月、下一個月的月曆
    :::spoiler Ans
       cal -3
    :::
:::