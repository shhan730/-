---
layout: post
title: "Git Ignore"
date: 2019-08-03
tag: [git]
author: Han-SeungHun
---



# GIT Ignore 설정하기



GIT Ignore란 무엇이고, 왜 필요한지, 어떻게 사용하는지 알아봅시다!



## GIT Ignore가 왜 필요할까?



Git 시스템을 사용하여 여러명이서 팀 작업을 진행할때

팀 내에서 공유되지 않기를 원하는 파일들이 생길 때가 있습니다.



예를 들자면 다음과 같은 상황들이 있습니다.


1. Eclipse 기반 프로젝트에서 “.classpath”와 “.project”를 공유하고 싶지 않은 경우

   해당 파일들은 내가 사용하는 PC를 기반으로 하여 각종 참조 경로들을 담고 있는 파일이기 때문에 공유할 필요가 없습니다.
   

2. MacOS 상에서 Git 사용시 ".DS_Store"을 공유하고 싶지 않은 경우

   해당파일들은 MacOS에서 Finder로 폴더에 접근하면 자동으로 생기는 파일로서, 해당 디렉토리의 특성, 구조 등에 관한 내용을 가지고 있는 파일입니다.
   따라서 공유할 필요가 없습니다.



이 외에도 [이곳]([https://www.gitignore.io](https://www.gitignore.io/))에 프로젝트에서 사용하고 있는 언어나 IDE, OS를 입력하면
일반적으로 해당환경에서 Ignore 해야하는 File들을 알려줍니다!



## GIT Ignore 적용하기



 GIT Ignore을 적용시키는 방법은 생각보다 매우 간단합니다.



1. 먼저 GIT 연동된 Folder 안으로 이동합니다.



2. ".gitignore" File을 생성합니다.



3. TextEditor를 이용해 ".gitignore" File을 편집합니다.
   


Ex)

~~~
.metadata/
.recommenders/
Servers/
.DS_Store
*/.DS_Store
~~~

다음과 같이 제외하고자 하는 File들을 Editor을 통해 작성합니다.

/ 표시는 하위의 모든 내용을 무시하겠다는 표시입니다!



## 수고하셨습니다!



이제 프로젝트를 Commit 해보세요!

Ignore 설정해 놓은 파일들이 이제 더이상 공유되지 않습니다.

수고하셨습니다!