# Day8 網路路由規劃

# 教材
+ https://www.netacad.com (上課使用)
+ https://www.skillsforall.com (自學資源)
+ http://10.10.53.198/

# 相關證照
+ 電腦硬體裝修
+ 網路架設
+ CCNA認證
+ win 11用戶端認證
+ Win Server認證
+ Linux認證
+ VM虛擬機器管理認證
+ 雲端系統認證
+ 資訊安全認證
    + 管理面
    + 技術面

# 課程主題：
+ 網路基礎、網路設備
   
+ CCNA練習

# 課程說明
+ 基礎
    + BCC (電腦基本概念Basic Computer Concepts)
    + 網路基礎
    + 佈線
        + 現代網路主要使用三種媒體來互連裝置
            + 纜線內的金屬線-數據被編碼為電子脈衝。
            + 纜線(光纖纜線)內的玻璃或塑膠纖維-數據被編碼成光脈衝。
            + 無線傳輸-數據透過調變為特定頻率的電磁波。
+ 應用
    + OS作業系統
        + Win10 (安全更新至202510)、Win11
        + MAC
        + win server
        + linux
    + 網路設備
        + Router
        + Switch
        + AP
        + Hub
    + 虛擬化
        + VM
    + 雲端技術
         
+ 進階
    + 資訊安全

# 課程內容
+ Cisco IOS
    + 使用者EXEC模式：提示字元為">"符號
    + 特權EXEC模式：提示字元為"#"符號
    + 使用者EXEC進入特權EXEC，輸入**enable**，離開使用**disable**或**exit**
    + 全域設定模式：裝置設定，特權EXEC模式下輸入**configure terminal**
    + 線路子設定模式，輸入**line**+管理線路類型和編號，退出使用**exit**，熱鍵為Ctrl+Z
    + 子設定模式切換：輸入**interface**
+ Packet Tracer練習
+ 裝置名稱及密碼設定
+ 設定檔
    + copy 複製檔案
    + reload 重開機
    + erase startup-config 刪除設定檔(設備還原或清除使用)

:::spoiler
   
CCNA1-ITN-2.5.5
【S1】
Switch>enable 切換至特權EXEC
Switch#configure terminal 切換至全域設定
Switch(config)#hostname S1 設定設備名稱
S1(config)#line console 0 至主控台
S1(config-line)#password letmein 設定密碼
S1(config-line)#login 儲存設定
S1(config-line)#exit 
S1(config)#enable password c1$c0 
S1(config)#enable secret itsasecret
S1(config)#banner motd #Warning#
S1(config)#service password-encryption 
S1(config)#exit
S1#show running-config 
S1#copy running-config startup-config 

【S2】
Switch>enable 
Switch#configure terminal 
Switch(config)#hostname S2
S2(config)#line console 0
S2(config-line)#password letmein
S2(config-line)#login
S2(config-line)#exit
S2(config)#enable password c1$c0
S2(config)#enable secret itsasecret
S2(config)#banner motd #Warning#
S2(config)#service password-encryption 
S2(config)#exit
S2#show running-config 
S2#copy running-config startup-config 

CCNA1-ITN-2.7.6

【S1】

Switch>enable 
Switch#configure terminal 
Switch(config)#hostname S1
S1(config)#line cons
S1(config)#line console 0
S1(config-line)#password cisco
S1(config-line)#login
S1(config-line)#exit
S1(config)#enable secret class
S1(config)#banner motd #Authorized access only. Violators will be 

prosecuted to the full extent of the law.#
S1(config)#interface vlan 1
S1(config-if)#ip address 192.168.1.253 255.255.255.0
S1(config-if)#no shutdown 
S1(config-if)#exit
S1(config)#exit
S1#copy running-config startup-config 


【S2】

Switch>enable 
Switch#configure terminal 
Switch(config)#hostname S2
S2(config)#line cons
S2(config)#line console 0
S2(config-line)#password cisco
S2(config-line)#login
S2(config-line)#exit
S2(config)#enable secret class
S2(config)#banner motd #Authorized access only. Violators will be 

prosecuted to the full extent of the law.#
S2(config)#interface vlan 1
S2(config-if)#ip address 192.168.1.253 255.255.255.0
S2(config-if)#no shutdown
S2(config-if)#exit
S2(config)#exit
S2#copy running-config startup-config

CCNA1-ITN-2.9.1-ASw

【ASw-1】

Switch>enable
Switch#configure terminal
Switch(config)#hostname ASw-1
ASw-1(config)#line console 0
ASw-1(config-line)#password xAw6k
ASw-1(config-line)#login
ASw-1(config-line)#line vty 0 15
ASw-1(config-line)#password xAw6k
ASw-1(config-line)#login
ASw-1(config-line)#exit
ASw-1(config)#enable secret 6EBUp
ASw-1(config)#service password-encryption
ASw-1(config)#banner motd #Warning#
ASw-1(config)#interface vlan 1
ASw-1(config-if)#ip address 10.10.10.100 255.255.255.0
ASw-1(config-if)#no shutdown
ASw-1(config-if)#exit
ASw-1(config)#exit
ASw-1#copy running-config startup-config

【ASw-2】

Switch>enable
Switch#configure terminal
Switch(config)#hostname ASw-2
ASw-2(config)#line console 0
ASw-2(config-line)#password xAw6k
ASw-2(config-line)#login
ASw-2(config-line)#line vty 0 15
ASw-2(config-line)#password xAw6k
ASw-2(config-line)#login
ASw-2(config-line)#exit
ASw-2(config)#enable secret 6EBUp
ASw-2(config)#service password-encryption
ASw-2(config)#banner motd #Warning#
ASw-2(config)#interface vlan 1
ASw-2(config-if)#ip address 10.10.10.100 255.255.255.0
ASw-2(config-if)#no shutdown
ASw-2(config-if)#exit
ASw-2(config)#exit
ASw-2#copy running-config startup-config

CCNA1-ITN-2.9.1-Class

【Class-A】

Switch>enable 
Switch#configure terminal 
Switch(config)#hostname Class-A
Class-A(config)#line console 0
Class-A(config-line)#password R4Xe3
Class-A(config-line)#login
Class-A(config-line)#line vty 0 15
Class-A(config-line)#password R4Xe3
Class-A(config-line)#login
Class-A(config-line)#exit
Class-A(config)#enable secret C4aJa
Class-A(config)#service password-encryption 
Class-A(config)#banner motd #Warning#
Class-A(config)#interface vlan 1
Class-A(config-if)#ip address 10.10.10.100 255.255.255.0
Class-A(config-if)#no shutdown 
Class-A(config-if)#end
Class-A#copy running-config startup-config 

【Class-B】

Switch>enable 
Switch#configure terminal 
Switch(config)#hostname Class-B
Class-B(config)#line console 0
Class-B(config-line)#password R4Xe3
Class-B(config-line)#login
Class-B(config-line)#line vty 0 15
Class-B(config-line)#password R4Xe3
Class-B(config-line)#login
Class-B(config-line)#exit
Class-B(config)#enable secret C4aJa
Class-B(config)#service password-encryption 
Class-B(config)#banner motd #Warning#
Class-B(config)#interface vlan 1
Class-B(config-if)#ip address 10.10.10.100 255.255.255.0
Class-B(config-if)#no shutdown 
Class-B(config-if)#end
Class-B#copy running-config startup-config 

CCNA1-ITN-2.9.1-Room

【S1】
Switch>enable
Switch#configure terminal
Switch(config)#hostname Room-145
Room-145(config)#line console 0
Room-145(config-line)#password 8ubRu
Room-145(config-line)#login
Room-145(config-line)#line vty 0 15
Room-145(config-line)#password 8ubRu
Room-145(config-line)#login
Room-145(config-line)#exit
Room-145(config)#enable secret C9WrE
Room-145(config)#service password-encryption
Room-145(config)#banner motd #Warning#
Room-145(config)#interface vlan 1
Room-145(config-if)#ip address 172.16.5.35 255.255.255.0
Room-145(config-if)#no shutdown
Room-145(config-if)#end
Room-145#copy running-config startup-config

【S2】
Switch>enable 
Switch#configure terminal 
Switch(config)#hostname Room-146
Room-146(config)#line console 0
Room-146(config-line)#password 8ubRu
Room-146(config-line)#login
Room-146(config-line)#line vty 0 15
Room-146(config-line)#password 8ubRu
Room-146(config-line)#login
Room-146(config-line)#exit
Room-146(config)#enable secret C9WrE
Room-146(config)#service password-encryption
Room-146(config)#banner motd #Warning#
Room-146(config)#interface vlan 1
Room-146(config-if)#ip address 172.16.5.40 255.255.255.0
Room-146(config-if)#no shutdown
Room-146(config-if)#end
Room-146#copy running-config startup-config
:::