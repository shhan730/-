---
layout: post
title: "Git Submodule 사용법"
date: 2019-08-02
tag: [git]
author: Han-SeungHun
---



# Git Sub Module 사용법



Git의 Sub Module을 사용하는 방법을 알아봅시다!



## Sub Module?



프로젝트를 수행하다 보면 다른 프로젝트를 함께 사용해야 하는 경우가 종종 있습니다!



예를 들자면

1. 외부에서 개발한 라이브러리를 사용하는 경우
2. 특정 라이브러리를 여러 프로젝트에서 공통으로 사용하는 경우

와 같은 상황입니다.



이러한 상황에서는 나의 프로젝트 안에서 다른 프로젝트나 라이브러리를 사용할 수 있어야 합니다.



이때, GIT의 Sub Module 기능을 사용하면 

나의 프로젝트안에 직접 외부 파일을 저장하지 않으면서도 외부 파일들을 불러와 사용할 수 있습니다.



그럼 이제 GIT에서 Sub Module을 사용하는 방법을 알아봅시다!



## Sub Module 사용법



Sub Module을 사용해 봅시다!



예제로 하위 프로젝트 여러 개를 가지는 프로젝트를 하나 만들어 서브모듈의 기능을 살펴봅시다!

작업할 Git 저장소에 Sub Module로 사용할 Git 저장소를 Sub Module로 추가해보자.



서브모듈을 추가하는 명령으로

 `git submodule add` 뒤에 추가할 저장소의 URL을 붙여주면 됩니다!

이 URL은 절대경로도 되고 상대경로도 됩니다.



예제로 “DbConnector” 라는 라이브러리를 추가해 보도록 하겠습니다!



* Command

~~~bash
$ git submodule add https://github.com/chaconinc/DbConnector
~~~



* Result

~~~bash
Cloning into 'DbConnector'...
remote: Counting objects: 11, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 11 (delta 0), reused 11 (delta 0)
Unpacking objects: 100% (11/11), done.
Checking connectivity... done.
~~~



기본적으로 서브모듈은 프로젝트 저장소의 이름으로 디렉토리를 만듭니다.

예제에서는 “DbConnector” 라는 이름으로 만들어 졌습니다.



서브보듈을 추가하고 난 후 `git status` 명령을 실행하면 몇 가지 정보를 알 수 있습니다.



* Command

~~~bash
$ git status
~~~



* Result

~~~bash
On branch master
Your branch is up-to-date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   .gitmodules
    new file:   DbConnector
~~~



우선 `.gitmodules` 파일이 만들어 졌네요!

이 파일은 서브디렉토리와 하위 프로젝트 URL의 매핑 정보를 담은 설정파일입니다



~~~bash
[submodule "DbConnector"]
    path = DbConnector
    url = https://github.com/chaconinc/DbConnector
~~~



서브모듈 개수만큼 이 항목이 생깁니다.

이 파일도 `.gitignore` 파일처럼 버전을 관리하며 다른 파일처럼 Push 하고 Pull 합니다.

이 프로젝트를 Clone 하는 사람은 `.gitmodules` 파일을 보고 어떤 서브모듈 프로젝트가 있는지 알 수 있습니다.



~~~
<NOTE>

gitmodules 파일에 있는 URL은 조건에 맞는 사람이면 누구든지 Clone 하고 Fetch 할 수 있도록 접근할 수 있어야 한다.

예를 들어 다른 사람이 Pull을 하는 URL과 라이브러리의 작업을 Push 하는 URL이 서로 다른 상황이라면 Pull URL이 모든 사람에게 접근 가능한 URL이어야 한다.

이러면 서브모듈 URL 설정을 덮어쓰기 해서 사용할 수 있는데,
git config submodule.DbConnector.url PRIVATE_URL 명령으로
다른 사람과는 다른 서브모듈 URL을 사용할 수 있다.

URL을 상대경로로 적을 수 있으면 상대경로를 사용하는 것이 낫다.
~~~



`.gitmodules` 은 살펴봤고 이제 프로젝트 폴더에 대해 살펴봅시다.



`git diff` 명령을 실행시키면 흥미로운 점을 발견할 수 있습니다.



* Command

~~~bash
$ git diff --cached DbConnector
~~~



* Result

~~~bash
diff --git a/DbConnector b/DbConnector
new file mode 160000
index 0000000..c3f01dc
--- /dev/null
+++ b/DbConnector
@@ -0,0 +1 @@
+Subproject commit c3f01dc8862123d317dd46284b05b6892c7b29bc
~~~



Git은 `DbConnector` 디렉토리를 서브모듈로 취급하기 때문에 해당 디렉토리 아래의 파일 수정사항을 직접 추적하지 않습니다.

대신 서브모듈 디렉토리를 통째로 특별한 커밋으로 취급합니다.

`git diff` 에 `--submodule` 옵션을 더하면 서브모듈에 대해 더 자세히 나옵니다.



* Command

~~~bash
$ git diff --cached --submodule
~~~



* Result

~~~bash
diff --git a/.gitmodules b/.gitmodules
new file mode 100644
index 0000000..71fc376
--- /dev/null
+++ b/.gitmodules
@@ -0,0 +1,3 @@
+[submodule "DbConnector"]
+       path = DbConnector
+       url = https://github.com/chaconinc/DbConnector
Submodule DbConnector 0000000...c3f01dc (new submodule)
~~~



이제 하위 프로젝트를 포함한 커밋을 생성하면 아래와 같은 결과를 확인할 수 있습니다.



* Command

~~~bash
$ git commit -am 'added DbConnector module'
~~~



* Result

~~~bash
[master fb9093c] added DbConnector module
 2 files changed, 4 insertions(+)
 create mode 100644 .gitmodules
 create mode 160000 DbConnector
~~~



`DbConnector` 디렉토리의 모드는 `160000`이다. Git에게 있어 160000 모드는 일반적인 파일이나 디렉토리가 아니라 특별하다는 의미입니다.



끝으로, Push 하면 끝입니다!



~~~bash
$ git push origin master
~~~





## 수고하셨습니다!



수고하셨습니다.

GIT의 Sub Module 사용법을 학습하셨습니다.

더 자세한 내용은 [이곳](https://git-scm.com/book/ko/v2/Git-도구-서브모듈)을 참고하세요!