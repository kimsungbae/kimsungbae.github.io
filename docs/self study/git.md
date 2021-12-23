---
layout: default
title: Gut
parent: Self Study
nav_order: 2
---

# Git
{: .no_toc }
 Git 공부 내용
 - 어렵고 헷갈리는 부분 위주로 공부
 - 중간 중간 새로 알게된 부분 추가 예정



## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Git란

Git은 파일 관리가 아닌 폴더(Directory) 관리 Tool
폴더(Directory)를 Git에서 관리
폴더(Directory)를 저장소(Repository)에 업그레이드해서 기능을 추가하기 전까지는 폴더(Directory)는 파일을 가지고 있는 그 이상도 아님.

## Git 시작하기 (commit, push, pull)

  1. 초기화 시점에 1회 입력
```shell
$ git init 
```

  2. 수정된 파일 commit하기
    - filname은 수정한 파일명
    - MESSAGE는 commit할때 수정한 부분을 부분 전달
```shell
$ git add <filenmae>
$ git commit -m 'MESSAGE'
```

  3. 지금까지 commit한 내용 원격저장소(GitHub)에 push
```shell
$ git push origin master
```

  4. 원격저장소(GitHub)에서 자료 복제하기
    - 원격저장소에서 URL 저장소 복사 후 터미널에서 실행
    - 터미널에서 원격저장소 자료 불러오기
```shell
$ git clone <URL>
$ git pull origin master
```

## branch (commit, push, pull)

  master만 쓰지 않고 branch해서 사용하는 이유

| 협업     | - 프로젝트는 혼자하기보다 협업으로 진행<br> - 각각의 팀원(branch)이 개발을 진행 후 하나로 통합(master)   |
|:------------|:-----------------------------------------------------------------------------------------------------------------------------------------|
| 버전    | - 현재 버전(master)말고 이후 버전에 대해서 개발을 진행할 때<br> - 핫픽스 진행|
| 도전    | - 기존 기능(master) 말고 새로운 기능을 추가하고 도전해볼 때<br> - 새로운 기능을 만들다가 괜찮으면 추가 아니면 버리기|
 위 기능이 다 가능한 이유는, 다른 branch에서 작업한 내용을 master로 commit 전에는 master에 영향을 주지 않음

  1. master
   간단히 말해서 내가 현재 보고 있는 곳을 master라고 할 수 있다.

  2. branch 만들기
   master말고 새로운 brunch 생성
```shell
$ git branch b1
```

  3. branch 기능
   
   - 현재 branch 시점 앞에는 *이 붙고, *이 안붙고 나온 branch는 현재 시점말고 나머지 branch들
 ```shell
$ git branch
```

   - 현재 내 시점을 b1 branch로 이동
 ```shell
$ git switch b1
```

   - b2 branch 삭제
 ```shell
$ git branch -d b2
```

  4. branch 병합
   
   - Fast Forward
   - Auto Merge
     - master와 branch b1이 다른 파일을 수정해서 겹치는 부분이 없을때
   - Conflit
     - master와 branch b1이 같은 파일을 동시에 수정
     - 어디서 수정한 내용을 적용할지 결정 필요

  5. branch collabo 실습
   
      1. github에서 레포지토리 생성
         1. github에서 만든게 origin이 main 사무실임
         2. 만들 때, .gitignore과 README.md 체크
         3. 같이 협업할 사람 넣어주기
         4. 링크 복사해서 직원들(A, B)한테 주기
      2. A와 B는 링크로 git-bash에서 링크 복사본 만들기
         1. 이름은 회사 규칙이 있음
         2. $ git clone <URL> A_collabo(레포지토리 이름)
         3. $ git clone <URL> B_collabo(레포지토리 이름)
      3. A는 login을 만들고, B는 signup을 만듬
      4. A와 B는 각각의 master에서 작업하는게 아닌 각각의 branch생성
         1. A는 feature/login, B는 feature/signup 라는 branch 생성
            - $ git switch -c feature/login
         2. 작업 시작
            - $ mkdir user #폴더 만들기(팀에서 해당 이름으로 폴더 만들자고 사전 협의)
            - $ touch login.py #파일 만들기(해당 파일에서 작업)
         3. 작업 끝나고 push하기(***origin master에 push 하면 안되고, origin feature/login이란 branch를 만들고 거기에 push***)
            - $ git push origin feature/login
      5. origin에서 PR(pull request) 생성
      6. 팀원들끼리 코드 리뷰 및 최종 merge 결정
         1. Auto merge 가능(초록생) => 진행
         2. Conflict 발생(빨간색) => github에서 수동으로 수정 후 merge 진행
      7. A는 master branch에서 origin master pull하기
         - $ git pull origin master
      8. 작업 반복