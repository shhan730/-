---
layout: post
title:  "Git branch 만들기"
date:   2019-07-30
tag: [git]
---
## 브랜치(branch)란?


브랜치란 영어로 나뭇가지, 지사, 분점 등을 뜻하는 단어인데요. 그 뜻과 일치하게 Git에서는 독립적으로 어떤 작업을 진행하기 위한 개념으로 쓰입니다.

팀 프로젝트에서 어떤 사람은 버그를 수정해야고 어떤 사람은 새로운 기능을 추가해야 할 때, 브랜치를 이용하면 동시에 같은 소스코드를 가지고 분리해서 작업을 할 수 있어요.

## Master 브랜치

`command line` 에 아래 명령을 입력하면 현재 브랜치를 확인할 수 있어요.

```bash
$git branch
*master
```

`*master` 라는 출력은 현재 내가 `master` 브랜치에서 작업하고 있다는 의미입니다. Git 저장소를 처음 만들면 Git은 바로 `master` 라는 이름의 브랜치를 만들어 줍니다. 

이 저장소에 새로운 파일을 추가하거나 파일의 내용을 변경하여 저장(커밋, `commit`)하는 것은 모두 `master` 브랜치에 기록됩니다. 

## 브랜치 만들기

하지만 일반적으로 `master` 브랜치에서만 모든 변경사항을 처리하는 것은 위험할 수 있습니다.

`master` 브랜치는 테스트를 통과한 에러가 없는 완전한 상태여야 한다는 정도로 생각해두고, 변경하고 싶을 땐 **항상** 브랜치를 따로 만들어서 변경한다는 점을 명심해야 합니다.

그러면 브랜치는 어떻게 만들 수 있을까요?

일반적으로 두 가지 방법이 있습니다.

### $git branch \<브랜치 이름\>

```bash
$git branch new_branch
$git branch
*master
new_branch
$git checkout new_branch
$git branch
master
*new_branch
```

Command line에 위의 명령을 따라 입력해보면, `*master` , `new_branch` 가 나타나는 것을 확인할 수 있습니다.

`master` 브랜치 앞에 `*(asterisk)` 가 붙어 있는 이유는 현재 `master` 브랜치에 있기 때문입니다. 또 `new_branch` 가 생겼는데, `$git branch new_branch` 라는 명령어로 브랜치를 생성한 것입니다.

`new_branch` 브랜치에서 작업하고 싶다면 `$git checkout` 명령어로 현재 작업하는 브랜치를 옮겨야 합니다. 

이 작업을 한번에 할 수 있을까요?

### $git checkout -b \<브랜치 이름\>

```bash
$git checkout -b test
$git branch
master
new_branch
*test
```

아까 전에 브랜치를 옮길때 사용한 `checkout` 명령어에 `-b` 옵션을 붙여 브랜치를 생성함과 동시에 생성한 브랜치로 옮길 수 있습니다.

