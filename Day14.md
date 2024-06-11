# Day14 網路路由規劃

# 課程內容
+ Ch9 位址解析
    + ARP位址解析協定
        + ARP快取，預設會儲存介於15~45秒
        + show ip arp(Cisco設備)：該指令用於顯示ARP表
        + ARP -a(win os command)
        + 群播MAC位址(多點傳送)：以 01-00-5e開頭
        + 廣播MAC位址：ff-ff-ff-ff-ff-ff
            + 網段內廣播、不分網段廣播(255.255.255.255)
            + 路由器會過濾掉廣播，只對區域網路有效
    + ARP欺騙
        + 
    + IPv6 沒有廣播，使用群播(多點傳送)，使用加入IPv6群組才會收到
        + IPv6 鄰居發現協定(ND、NDP)：使用ICMPv6為IPv6提供位址解析、路由器發現和重導向服務。
        + 一組位址以:分隔，以16進位表示


:::info
+ 10.2.5 語法檢查-設定介面
    + 進入全域設定模式。
    + R1#configure terminal
    + Enter configuration commands, one per line. End with CNTL/Z.
    + 設定 gigabitethernet 0/0/0 介面。
        + R1(config)#interface gigabitethernet 0/0/0

    + 將鏈路加上 'Link to LAN' 的描述。
        + R1(config-if)#description Link to LAN

    + 使用 IPv4 位址 192.168.10.1 和網路遮罩 255.255.255.0 設定介面。
        + R1(config-if)#ip address 192.168.10.1 255.255.255.0

    + 使用 IPv4 位址 2001:db8:acad:10::1 和前置碼長度 /64 設定介面。
        + R1(config-if)#ipv6 address 2001:db8:acad:10::1/64
    + 啟用介面並返回全域設定模式。
        + R1(config-if)#no shutdown

    + \*Aug 1 01:43:53.435: %LINK-3-UPDOWN: Interface GigabitEthernet0/0/0, changed state to down
    + \*Aug 1 01:43:56.447: %LINK-3-UPDOWN: Interface GigabitEthernet0/0/0, changed state to up
    + \*Aug 1 01:43:57.447: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0, changed state to up
        + R1(config-if)#exit
        + R1#
    + 您已成功設定路由器 R1 上的初始設定。
:::

:::info
+ CCNA1-ITN-10.3.4-new

+ 1.連線
+ 2.設定PCA和PCB的位址
  點PCA
  點【IP Configuration】
+ 3.ping測試
  點PCA
  點【Command Prompt】
  輸入:
    ping 192.168.0.3
+ 4.ping為何無法成功?
  未設定路由器
  按【summit】
+ 5.路由器基本設定及介面IP設定
Router>enable
Router#configure terminal 
Router(config)#hostname R1
R1(config)#enable secret class
R1(config)#line console 0
R1(config-line)#password cisco
R1(config-line)#login
R1(config-line)#exit
R1(config)#service password-encryption 
R1(config)#banner motd #unauthorized access is prohibited#
R1(config)#interface g0/0/0
R1(config-if)#ip address 192.168.0.1 255.255.255.0
R1(config-if)#no shutdown 
R1(config-if)#interface g0/0/1
R1(config-if)#ip address 192.168.1.1 255.255.255.0
R1(config-if)#no shutdown 
R1(config-if)#end
R1#copy running-config startup-config 
+ 6.ping測試
  點PCA
  點【Command Prompt】
  輸入:
    ping 192.168.0.3

+ 7.ping為何能成功?
  已設定路由器
  按【summit】

+ 8.設定交換器
Switch>enable 
Switch#configure terminal 
Switch(config)#hostname S1
S1(config)#enable secret class
S1(config)#line console 0
S1(config-line)#password cisco
S1(config-line)#login
S1(config-line)#exit
S1(config)#service password-encryption 
S1(config)#banner motd #unauthorized access is prohibited#
S1(config)#interface vlan 1
S1(config-if)#ip address 192.168.1.2 255.255.255.0
S1(config-if)#no shutdown 
S1(config-if)#exit
S1(config)#ip default-gateway 192.168.1.1
S1(config)#exit
S1#copy running-config startup-config 
+ 9.設定R1的安全遠端存取連線(SSH)
R1>enable 
Password:       class
R1#configure terminal 
R1(config)#ip domain-name academy.net
R1(config)#crypto key generate rsa
How many bits in the modulus [512]: 1024
R1(config)#username SSHuser secret cisco
R1(config)#line vty 0 4
R1(config-line)#login local
R1(config-line)#transport input ssh

+ 10.驗證ssh遠端存取
  點PCA
  點【Command Prompt】
  輸入:
    ssh -l SSHuser 192.168.1.1
    Password:cisco

+ 12.問答
  1.若g0/0/1被關閉，啟用介面的指令?
    no shutdown

  2.若R1 g0/0/1的ip設定為192.168.1.2會發生什麼?
    無法連線遠端裝置
:::

:::info
CCNA1-ITN-10.3.5
錯誤點
1.PC1 IP設錯

2.1.PC4 Default Gateway設錯

3.S1未設定Default Gateway

S1>enable 
S1#show running-config
S1#configure terminal 
S1(config)#ip default-gateway 192.168.10.1

4.S2未設定IP

S2>enable
S2#show running-config 
S2#configure terminal
S2(config)#interface vlan 1
S2(config-if)#ip address 192.168.11.2 255.255.255.0

:::

:::info
CCNA1-ITN-10.4.3-Collage
+ College

Router>enable 
Router#configure terminal 
Router(config)#hostname College
College(config)#line console 0
College(config-line)#password cisco
College(config-line)#login
College(config-line)#line vty 0 4
College(config-line)#password cisco
College(config-line)#login
College(config)#enable secret class
College(config)#service password-encryption 
College(config)#banner motd #Warning#
College(config)#ipv6 unicast-routing 
College(config)#interface g0/0
College(config-if)#description Link to Class-A
College(config-if)#ip address 128.107.20.1 255.255.255.0
College(config-if)#ipv6 address 2001:db8:a::1/64
College(config-if)#ipv6 address fe80::1 link-local 
College(config-if)#no shutdown 
College(config-if)#interface g0/1
College(config-if)#description Link to Class-B
College(config-if)#ip address 128.107.30.1 255.255.255.0
College(config-if)#ipv6 address 2001:db8:b::1/64
College(config-if)#ipv6 address fe80::1 link-local 
College(config-if)#no shutdown 
College(config-if)#end
College#copy running-config startup-config 


+ Class-B (ip評分會錯)
Switch>enable 
Switch#configure terminal 
Switch(config)#hostname Class-B
Class-B(config)#line console 0
Class-B(config-line)#password cisco
Class-B(config-line)#login
Class-B(config-line)#line vty 0 15
Class-B(config-line)#password cisco
Class-B(config-line)#login
Class-B(config-line)#exit
Class-B(config)#enable secret class
Class-B(config)#service password-encryption 
Class-B(config)#banner motd #Warning#
Class-B(config)#interface vlan 1
Class-B(config-if)#description IP
Class-B(config-if)#ip address 128.107.30.10 255.255.255.0
Class-B(config-if)#no shutdown 
Class-B(config-if)#end
Class-B#copy running-config startup-config 


PC
1.ipv6預設閘道要用 link-local位址
2.pc4的ip要修正
:::

:::info
CCNA1-ITN-10.4.3-RTA

RTA(ipv6位址錯誤)

Router>enable 
Router#configure terminal
Router(config)#hostname RTA
RTA(config)#line console 0
RTA(config-line)#password cisco
RTA(config-line)#login
RTA(config-line)#line vty 0 4
RTA(config-line)#password cisco
RTA(config-line)#login
RTA(config-line)#exit
RTA(config)#enable secret class
RTA(config)#service password-encryption 
RTA(config)#banner motd #Warning#
RTA(config)#ipv6 unicast-routing 
RTA(config)#interface g0/0
RTA(config-if)#description Link to ASw-1
RTA(config-if)#ip address 10.10.10.1 255.255.255.0
RTA(config-if)#ipv6 address 2001:db8:acad:100::1/64
RTA(config-if)#ipv6 address fe80::1 link-local 
RTA(config-if)#no shutdown 
RTA(config-if)#interface g0/1
RTA(config-if)#description Link to ASw-2
RTA(config-if)#ip address 10.10.11.1 255.255.255.0
RTA(config-if)#ipv6 address 2001:db8:acad:200::1/64
RTA(config-if)#ipv6 address fe80::1 link-local 
RTA(config-if)#no shutdown
RTA(config-if)#end
RTA#copy running-config startup-config 


ASw-2

Switch>enable 
Switch#configure terminal 
Switch(config)#hostname ASw-2
ASw-2(config)#line console 0
ASw-2(config-line)#password cisco
ASw-2(config-line)#login
ASw-2(config-line)#line vty 0 15
ASw-2(config-line)#password cisco
ASw-2(config-line)#login
ASw-2(config-line)#exit
ASw-2(config)#enable secret class
ASw-2(config)#service password-encryption 
ASw-2(config)#banner motd #Warning#
ASw-2(config)#inter
ASw-2(config)#interface vlan 1
ASw-2(config-if)#description Switch Self ip
ASw-2(config-if)#ip address 10.10.11.100 255.255.255.0
2001:db8:acad:200::100/64
ASw-2(config-if)#no shutdown 
ASw-2(config-if)#exit
ASw-2(config)#ip default-gateway 10.10.11.1
ASw-2(config)#interface vlan 1
ASw-2(config-if)#end
ASw-2#copy running-config startup-config
:::


