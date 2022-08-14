NETWORK
=======

![image](https://user-images.githubusercontent.com/109789864/184523234-a93763e7-aaba-4fcf-a113-70ddd1912ca0.png)

![image](https://user-images.githubusercontent.com/109789864/184523260-9344f320-fbfd-4c44-ae42-cb8a6fe6069a.png)

ch1.pacp 파일을 wireshark로 열어보니 이렇게 나왔는데 

![image](https://user-images.githubusercontent.com/109789864/184523280-a9cd1682-3670-46bc-85dc-178452d04301.png)

일단 TCP stream으로 열어봤더니 바로 정답이 나왔다

![image](https://user-images.githubusercontent.com/109789864/184523342-be3242e7-ec01-4dfe-a16d-ada808ca95d3.png)

![image](https://user-images.githubusercontent.com/109789864/184523363-b8b20e6b-44e9-40cb-958d-2c35a3241257.png)

ch2.pcap 파일을 열어서 봤더니 TELNET이라는 Protocol이 눈에 띄었음

![image](https://user-images.githubusercontent.com/109789864/184523400-9053924c-45e4-452d-8e88-e8e61b9cf357.png)

바로 TCP stream을 열어서 봤더니 Password가 나왔다

![image](https://user-images.githubusercontent.com/109789864/184523437-79224811-ff2d-46de-bb6c-b71502f7ad65.png)

![image](https://user-images.githubusercontent.com/109789864/184523450-c50623c4-f077-4170-ad55-621b548dc2e2.png)

start the challenge를 눌렀더니 16진수가 나와서 HxD에 넣어봤다

![image](https://user-images.githubusercontent.com/109789864/184523492-cd4af072-8b13-45e6-976e-43392636e726.png)

그랬더니 Authorization: Basic 뒤에 Base64 text가 있어서 디코더했다

![image](https://user-images.githubusercontent.com/109789864/184523524-5241994d-7261-4810-8d32-c24c3b331597.png)

![image](https://user-images.githubusercontent.com/109789864/184523547-098c9d3a-3b95-4436-a773-c14d46cdb404.png)

ch3.pcap파일을 열어보니 하나가 나왔다

![image](https://user-images.githubusercontent.com/109789864/184523576-7b6254d0-f148-4398-8b49-644c8b692f1d.png)

![image](https://user-images.githubusercontent.com/109789864/184523584-62c0ef61-095a-4d88-8567-478c21e46e15.png)

바로 TCP stream으로 열어서 봤더니 Authorization: Basic dXNlcnRlc3Q6cGFzc3dvcmQ= 저번 문제와 같이 Base64 text가 나왔다
그래서 바로 디코더 해줬다

![image](https://user-images.githubusercontent.com/109789864/184523644-31cc9c7c-e87c-4588-ae28-785e3647f2ae.png)
 
바로 플래그가 나왔다

![image](https://user-images.githubusercontent.com/109789864/184524141-2d73073a-858e-4c19-90e1-37fe6975871f.png)

![image](https://user-images.githubusercontent.com/109789864/184524175-edde422c-5cd9-4512-b293-82e4545d5c5b.png)

ch18.bin파일을 wireshark로 열었다

![image](https://user-images.githubusercontent.com/109789864/184524231-7c40b640-d5c9-448d-b2d3-b5d85f5b442d.png)

Wireless 옵션으로 

![image](https://user-images.githubusercontent.com/109789864/184523714-acaa2a8b-f577-431c-bb5a-de8847626819.png)

start the challenge를 누르면 시스코 하드웨어 정보들이 나와있다

-------------------------------------------------------------
!
! Last configuration change at 13:41:43 CET Mon Jul 8 2013 by admin
! NVRAM config last updated at 11:15:05 CET Thu Jun 13 2013 by admin
!
version 12.2
no service pad
service password-encryption
!
isdn switch-type basic-5ess
!
hostname rmt-paris
!
security passwords min-length 8
no logging console
enable secret 5 $1$p8Y6$MCdRLBzuGlfOs9S.hXOp0.
!
username hub password 7 025017705B3907344E 
username admin privilege 15 password 7 10181A325528130F010D24
username guest password 7 124F163C42340B112F3830
!
!
ip ssh authentication-retries 5
ip ssh version 2
!
interface BRI0/0
 ip address 192.168.1.2 255.255.255.0
 no ip directed-broadcast
 encapsulation ppp
 dialer map ip 192.168.1.1 name hub broadcast 5772222
 dialer-group 1
 isdn switch-type basic-5ess
 ppp authentication chap callin
 no shutdown
!
!
interface GigabitEthernet1/15
 ip address 192.168.2.1 255.255.255.0
 no shutdown
!
router bgp 100
 no synchronization
 bgp log-neighbor-changes
 bgp dampening
 network 192.168.2.0 mask 255.255.255.0
 timers bgp 3 9
 redistribute connected
!
ip classless
ip route 0.0.0.0 0.0.0.0 192.168.1.1
!
!
access-list 101 permit ip any any
dialer-list 1 protocol ip list 101
!
no ip http server
no ip http secure-server
!
line con 0
 password 7 144101205C3B29242A3B3C3927
 session-timeout 600
line vty 0 4
 session-timeout 600
 authorization exec SSH
 transport input ssh
 
-------------------------------------------------------------

username hub password 7 025017705B3907344E 
username admin privilege 15 password 7 10181A325528130F010D24
username guest password 7 124F163C42340B112F3830

이 부분이 암호화 되어있어서 암호화를 풀어보면 

![image](https://user-images.githubusercontent.com/109789864/184523800-efb94735-4d1d-42b7-a6bc-1a5b7678424e.png)
![image](https://user-images.githubusercontent.com/109789864/184523810-430dd2d8-d07f-4a9f-a682-20a65a2b1881.png)
![image](https://user-images.githubusercontent.com/109789864/184523817-9fcd25c7-cbd6-4dd6-8210-aa17bd91ccb3.png)

그럼 enable의 password는 6sK0_enable이다

![image](https://user-images.githubusercontent.com/109789864/184523849-8e3d3536-7225-4ccb-bc4b-627fee19f664.png)

![image](https://user-images.githubusercontent.com/109789864/184523918-f72037df-03c9-4624-b57d-90157120487e.png)

dig 명령을 이용해서 풀어주었다

---------------------------------------------------------------------------------
@는 확인할 네임서버를 지정하는 곳이다. ip가 올수도 있고 저렇게 이름이 올 수도 있다

-p는 포트 번호를 넣는 것이다

그리고 뒤에 ch11.challenge01.root-me.org 는 도메인 호스트 이름이다

-t는 타입을 설정하는 것이고

axfr은 zone transfer ( authority를 갖는 특정 네임서버에 질의 ) 라고 한다

zone transfer : 해당 도메인의 zone 에 대한 복사본을 얻기 위해,primary 로부터 zone 데이타베이스를 끌어오는 작업

---------------------------------------------------------------------------------

![image](https://user-images.githubusercontent.com/109789864/184524037-03b35761-b7ab-4997-84a0-d8278b28738a.png)

![image](https://user-images.githubusercontent.com/109789864/184524045-38637ec3-3777-4347-9af1-d93e0a46a918.png)

패킷이 도달하지 못한 것이 많은데 ttl=13부터 정상작동이 된다
flag: 13

![image](https://user-images.githubusercontent.com/109789864/184524090-843897e7-7d83-4dbf-ae8c-cf576da23e16.png)

얘도 굉장히 쉽게 ldapsearch를 쓰면 구할 수 있다

![image](https://user-images.githubusercontent.com/109789864/184524114-64818e75-419d-4d77-bed8-5df9111a11df.png)

