---
layout: post
title: 'Jekyll Chirpy 테마 깃허브 블로그 만들기'
description: jekyll chirpy gitblog
tags: jekyll gitblog
categories: Gitblog
date: '2023-01-01 00:00:00 +0900'
---

> 깃허브 블로그를 진행해 봐야겠다는 생각만 수차례, deploy 오류만 수차례 이제서야 첫 글을 작성합니다.  
> (어쩌다보니 새해 첫글이 되버렸네요)  
> 해당글은 Github 사용법 및 마크다운 문법등의 다른 부가적인 정보들을 제공하지 않습니다.  
> Github 및 Jekyll Chirpy 테마로 블로그를 만드는 것에 대하여만 정보 제공합니다.  
> MacOS 기준으로 작성되며 작성 시점기준 Apple M1, Ventura 13.1 을 사용중입니다.  

## 테마 설치하기
---
chirpy 테마는 아래 방법들로 설치할 수 있습니다.
1. [Chirpy starter](https://github.com/cotes2020/chirpy-starter/generate){:target="_blank"}를 통해 직접 설치  
  공식 레포에서도 해당 방법을 제안하나 그러나 저는 생각만큼 간단하게 되지 않았고 deploy 과정에서 여러 문제점들을 겪어 해당방법을 사용하지 않았습니다.  

1. [Github](https://github.com/cotes2020/jekyll-theme-chirpy){:target="_blank"}에서 소스를 fork 받아서 만들기  
  공식 레포를 fork해서 사용하는 방법으로 Git에 대한 기본이해가 필요하나 커스터마이징을 하기 위해서는 해당 방법을 추천합니다.  
  해당 글에서는 이 방식을 사용하여 진행합니다.  

### Repo Fork
[Fork Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy/fork){:target="_blank"} 를 사용하여 fork 받습니다.  
아래 보이는 사진처럼 Repository name을 `<github 아이디>.github.io` 형태로 구성합니다.  
Stable 한 환경을 구성하기 위하여 `master branch only `는 체크해제 해줍니다.  
![fork](/assets/img/gitblog/chirpy-fork.png){:style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px;"}

### Repo Clone
아래 명령어를 통하여 Fork한 레포지토리를 clone 받습니다.  
```zsh
git clone https://github.com/<Github-UserName>/<Github-UserName>.github.io.git
# ex) git clone https://github.com/Jintopia/Jintopia.github.io.git
```
정상적으로 로컬로 소스를 받았다면 해당 경로로 이동하여 아래 명령어를 통해 version 고정을 해줍니다.


## 로컬 환경 설정하기
---
로컬에서 Jekyll을 실행하기 위해서는 ruby가 필수적이기 때문에 아래 명령어를 사용하여 ruby를 설치합니다.  
Github에 commit 전 실행시켜 환경 설정이나 포스팅 결과를 미리 확인하기 위함입니다.