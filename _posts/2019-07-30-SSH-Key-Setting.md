---
layout: post
title: "SSH Key Settings"
date: 2019-07-30
tag: [git]
author: Han-SeungHun
---



# SSH 공개 Key 만들기

많은 Git 서버들은 SSH 공개 Key로 인증합니다.

일단 공개 Key를 만들어 봅시다!

일단 Key가 이미 있는지 확인해 보도록 하겠습니다.



## Key 가 이미 있는지 확인하는 법



사용자의 SSH 키들은 기본적으로 사용자의 `~/.ssh` 디렉토리에 저장합니다.

그래서 만약 디렉토리의 파일을 살펴보면 공개키가 있는지 확인할 수 있습니다.



* Command

~~~bash
$ cd ~/.ssh
$ ls
~~~



* Result

~~~bash
authorized_keys2  id_dsa       known_hosts
config            id_dsa.pub
~~~



만약 Key가 이미 존재한다면 

something, something.pub이라는 형식으로 된 파일을 볼 수 있습니다.

something은 보통 `id_dsa`나 `id_rsa`라고 되어 있습니다.

그 이유는 SSH Key가 Support 하는 Protocol에는 4가지가 있는데

| Protocol | Generation |
| :------: | :--------: |
|   RSA    |     1      |
|   DSA    |     2      |
|  ECDSA   |     3      |
| ed25519  |     4      |

이중에서 가장 많이 사용되는 Protocol이 RSA, DSA 이기 때문입니다.

id_ 뒤에 따라나오는 단어가 바로 여러분의 SSH키의 Protocol 입니다.

더 자세한 내용은 [여기](https://en.wikipedia.org/wiki/Ssh-keygen)를 참고하세요!



이러한 Key들 중 `.pub`파일이 공개키이고 다른 파일은 개인키입니다.

**만약 이 파일이 없거나 `.ssh` 디렉토리도 보이지 않으면 키를 새로 생성해야 합니다.**




## Key 생성하기

Key 가 없을 경우 Key를 생성하여 봅시다!



SSH 키는 `ssh-keygen`이라는 프로그램으로 생성합니다.

 `ssh-keygen` 프로그램은 Linux, Mac은 SSH 패키지에 포함돼 있고 Windows는 MSysGit 패키지 안에 들어 있습니다.



* Command

~~~bash
$ ssh-keygen
~~~



* Result

~~~bash
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/schacon/.ssh/id_rsa):
~~~



터미널에 `ssh-keygen` 이라 입력하면 Key 의 저장 위치를 입력하라고 요청합니다.

우리가 저장할 경로인 `.ssh/id_rsa` 입력합시다.



* Result

~~~bash
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
~~~



이후 앞으로 사용할 암호를 2번 입력합니다.

만약 암호를 입력하지 않으면 키를 사용할 때 암호를 묻지 않습니다.


* Result

~~~bash
Your identification has been saved in /Users/schacon/.ssh/id_rsa.
Your public key has been saved in /Users/schacon/.ssh/id_rsa.pub.
The key fingerprint is:
43:c5:5b:5f:b1:f1:50:43:ad:20:a6:92:6a:1f:9a:3a schacon@agadorlaptop.local
~~~



이러한 메세지가 나오면 성공입니다!



## GIT에 SSH Key 등록하기



자, 이제 GIT에 해당 코드를 등록하여 봅시다!



### 먼저 해당 Key를 복사합니다!



* Command

~~~bash
$ cat ~/.ssh/id_rsa.pub
~~~



해당 명령어를 입력하면 우리가 저장해 두었던 Key 내용이 열립니다.



* Result

~~~bash
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAklOUpkDHrfHY17SbrmTIpNLTGK9Tjom/BWDSU
GPl+nafzlHDTYW7hdI4yZ5ew18JH4JW9jbhUFrviQzM7xlELEVf4h9lFX5QVkbPppSwg0cda3
Pbv7kOdJ/MTyBlWXFCR+HAo3FXRitBqxiX1nKhXpHAZsMciLq8V6RjsNAQwdsdMFvSlVK/7XA
t3FaoJoAsncM1Q9x5+3V0Ww68/eIFmb1zuUFljQJKprrX88XypNDvjYNby6vw/Pb0rwert/En
mZ+AW4OZPnTPI89ZPmVMLuayrD2cE86Z/il8b+gw3r3+1nKatmIkjn2so1d01QraTlMqVSsbx
NrRFi9wrf+M7Q== schacon@agadorlaptop.local
~~~



이런식으로 말이죠!

ssh-rsa 부분부터 끝까지 복사합시다!



### 자, 이제 자신의 GIT 계정에 Key를 등록해 봅시다!



**먼저, GITHUB(https://github.com/) 에 접속해 봅시다!**

* GITHUB 계정이 없다면 생성 후 로그인 합시다!
* GITHUB 계정이 있다면 로그인 하세요!




1. 위쪽 상단에 있는 아이콘을 클릭한 후 Settings 에 들어갑니다.


<img src="{{ '/assets/img/image_main.jpg'}}">



2. Personal Settings 에 SSH and GPG keys 에 들어갑니다.


<img src="{{ '/assets/img/image_personalSettings.png'}}">


3. 상단 New SSH Key를 선택합니다.


<img src="{{ '/assets/img/image_newSSHBtn.png'}}">


4. Title에 Key의 이름을 입력한 후 Key에 위에서 복사한 내용은 붙여넣기 합니다.


<img src="{{ '/assets/img/image_addKey.png'}}">


5. 마지막으로 Add SSH key를 눌러 Key를 추가해 줍니다!



## 수고하셨습니다!

자, 이제 GIT에서 SSH키를 사용할 준비가 끝났습니다.

GIT 강의로 넘어가서 계속 진행해 주세요!