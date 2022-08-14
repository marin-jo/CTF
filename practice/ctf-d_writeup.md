Forensic
========

![image](https://user-images.githubusercontent.com/109789864/184524297-c2747af7-cc33-40f8-9172-3f86e28b1239.png)

![hidden](https://user-images.githubusercontent.com/109789864/184524316-e73f26ba-c5ff-4cc0-a7f5-a19c54397d06.jpg)

이런 사진이 하나 있는데 forensically로 명도 조절했더니

![image](https://user-images.githubusercontent.com/109789864/184524391-4bc56c1f-e717-4794-84ed-5199a06fff22.png)

플래그가 나왔다
flag: tjctf{th3_f0x_jump3d_0v3r_m3}

![image](https://user-images.githubusercontent.com/109789864/184524405-5aa909f6-b62f-4fb6-adcd-c8747d998a10.png)

![just_open_it](https://user-images.githubusercontent.com/109789864/184524427-0d63df65-4733-4bf6-bb58-8ec8cafc73e1.jpg)

이런 사진을 줬는데 사진만으로는 아무것도 나오지 않았다
그래서 HxD로 살펴봤다

![image](https://user-images.githubusercontent.com/109789864/184524460-e26a6398-3882-43e0-8606-7e97f5e74684.png)

바로 format에 나와있는 ABCTF를 검색해더니 나왔다

![image](https://user-images.githubusercontent.com/109789864/184524471-77b42c40-18a9-4dd3-98ce-d192395c5721.png)

![hidden](https://user-images.githubusercontent.com/109789864/184524498-19de5a49-9154-4e8c-a8b8-bd0bcc240119.png)

이런 강아지 사진이 나와있는데 stegsolve로 한번 열어서 빨간색이 이상해보인다고 해서 Red plane을 0으로 설정했다

![image](https://user-images.githubusercontent.com/109789864/184524528-62b002b9-bc3a-4408-a0f1-edbe49f70381.png)

바로 플래그가 나왔다

![image](https://user-images.githubusercontent.com/109789864/184524543-80a4f45f-ce7b-4aca-8714-fc1337ed5117.png)

![image](https://user-images.githubusercontent.com/109789864/184524574-57a51c6e-d095-459b-a567-d3f58db7b3a7.png)

파일을 열어서 봤더니 앞에 시그니처가 gz였다
그래서 확장자를 gz로 주었다

![image](https://user-images.githubusercontent.com/109789864/184524637-0e853228-0d08-42b4-a275-a90522a333fe.png)

그러고 열었더니 플래그가 나왔다
