# Day10 網路路由規劃

# 教材資源內容
+ 網路表示方式
    + 網路介面卡 (NIC) -NIC 實際將終端裝置連線到網路。
    + 實體埠 - 網路設備上的介面或插座，網路媒體透過它連接到主機或其他網路設備
    + 介面 - 網間設備上連接到個別網路的專用埠由於路由器連接網路，因此路由器上的連接埠稱為網路介面。==註: 通常，術語連接埠和介面可互換使用==

+ 拓樸圖
    + 拓樸圖是任何使用網路的人都必須提供的文件。它們提供網路連線方式的視覺圖。
        + 實體拓撲圖：說明中介裝置和電纜安裝的實體位置
        + 邏輯拓撲圖：說明設備，連接埠和網路的定址方案

# 課程內容
+ 訊息傳遞方式
    + 協定和模型
        + 通訊協定需求
            + 編碼：網路訊息->傳送主機轉換成位元；目的主機接收解碼。
                + 訊息編碼為封包經由傳輸介質(通道)送出
                + IP(Internet protocols)網際網路通訊協定
            + 格式化和封裝：當訊息從來源傳送到目的地時，使用特定的格式或結構。格式取決於訊息類型和傳遞通道。
                 + IPv4、IPv6
                     + 版本、流量類別(分類)、流標籤、負載長度、標頭、跳躍數的限制(避免封包到處跑)、來源IP、目的IP，每個位址128位元，有4個byte
                     + IPv6 40 byte
            + 大小
                + 訊息封包分割
            + 時間與時機
                + 網路傳輸分半雙工、全雙工
                + 流量控制：管理傳輸速率
                + 回應逾時：等待回應的時間
                + 存取方式：決定可以傳輸訊息的時間
            + 傳送訊息
                + 單點傳送
                + 多點傳送
                + 廣播
    + 通訊協定類型
        + 網路通訊協定
            + IP、傳輸控制TCP、HTTP
            + 應用層Telnet(無加密)、SSH(加密)
            + 通訊層SSL負責通訊加密
            + 傳輸層安全性TLS協定
        + 路由通訊協定
            + OSPF路由協定(最短路徑優先)
            + 不同網路公司單位交換路由BGP協定
        + 服務發現協定
            + DHCP自動取得主機組態設定，主要用來分配IP
            + DNS：將網址轉為IP、IP反查網址驗證

    + 通訊協定功能
        + 定址：IP協議
        + 可靠性：TCP協議保證傳送協定
        + 流量控制：傳輸過程雙方速度不同，TCP提供流量控制
        + 順序性：封包切割後依序號重組，TCP提供排序
        + 錯誤偵測：處理確認資料損壞
        + 應用程式開發介面：
            + 例：開網頁
                |TCP/IP層|通訊協議|處理|
                |--|--|--| 
                | 應用層     | HTTP     | 控制訊息之間的傳送   |
                | 傳輸層     | TCP      | 流量控制、可靠性控制 |
                | 網際網路層 | IP       | 定址                 |
                | 網路存取層 | 乙太網路 |                      |

    + TCP/IP通訊協定堆疊
    ![tcp_ip](https://hackmd.io/_uploads/rJFVZ6CVR.png)

    