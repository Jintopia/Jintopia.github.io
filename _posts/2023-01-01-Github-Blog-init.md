---
layout: post
title: 'Jekyll 깃허브 블로그 생성부터 배포까지'
description: jekyll gitblog chirpy
tags: Jekyll Gitblog
categories: Gitblog
date: '2023-01-01 00:00:00 +0900'
img_path: /assets/img/gitblog
---

> 깃허브 블로그를 진행해 봐야겠다는 생각만 수차례, deploy 오류만 수차례 이제서야 첫 글을 작성합니다.  
> (어쩌다보니 새해 첫글이 되버렸네요)  
> 해당글은 Github 사용법 및 마크다운 문법등의 다른 부가적인 정보들을 제공하지 않습니다.  
> Github 및 Jekyll Chirpy 테마로 블로그를 만드는 것에 대하여만 정보 제공합니다.  
> MacOS 기준으로 작성되며 작성 시점기준 Apple M1, Ventura 13.1 을 사용중입니다.  

## 설치방법
---
chirpy 테마는 아래 방법들로 설치할 수 있습니다.
1. [Chirpy starter](https://github.com/cotes2020/chirpy-starter/generate){:target="_blank"}를 통해 직접 설치  
  공식 레포에서도 해당 방법을 제안하나 그러나 저는 생각만큼 간단하게 되지 않았고 deploy 과정에서 여러 문제점들을 겪어 해당방법을 사용하지 않았습니다.  

1. [Github](https://github.com/cotes2020/jekyll-theme-chirpy){:target="_blank"}에서 소스를 fork 받아서 만들기  
  공식 레포를 fork해서 사용하는 방법으로 `Git`에 대한 기본이해가 필요하나 커스터마이징을 하기 위해서는 해당 방법 사용합니다.  
  해당 글에서는 이 방식을 사용하여 진행합니다.  

### Repo Fork
[Fork Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy/fork){:target="_blank"} 를 사용하여 fork 받습니다.  
아래 보이는 사진처럼 Repository name을 `<github 아이디>.github.io` 형태로 구성합니다.  
Stable 한 환경을 구성하기 위하여 `master branch only`는 체크해제 해줍니다.  
![fork](chirpy-fork.png){:style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px;"}

### Repo Clone
아래 명령어를 통하여 Fork한 레포지토리를 clone 받습니다.  
```zsh
git clone https://github.com/<Github-UserName>/<Github-UserName>.github.io.git
# ex) git clone https://github.com/Jintopia/Jintopia.github.io.git
```
정상적으로 로컬로 소스를 받았다면 로컬경로로 이동하여 아래 명령어를 통해 lastest tag로 고정해줍니다.  
(글 작성기준 `v5.4.0`) 이후 chirpy 초기화를 진행하면 기본적인 준비는 모두 끝났습니다.
```zsh
git reset --hard tags/v5.4.0 # git reset --hard tags/<TAG-Version>
tools/init.sh
[INFO] Initialization successful!  # 해당 메시지가 출력되면 정상적으로 초기화가 진행된것입니다.
# 해당 메시지가 출력되지 않았을 경우 아래 문제 해결란을 참고해주세요.
```

### Run Locally
로컬에서 Jekyll을 실행하기 위해서는 ruby가 필수적이기 때문에 아래 명령어를 사용하여 rbenv를 설치합니다.  
rbenv는 루비의 버전을 독립적으로 사용할 수 있도록 도와주는 패키지입니다. 아나콘다와 유사하게 생각하시면 됩니다.  
참고 : <https://jekyllrb.com/docs/installation/>{:target="_blank"} 
```zsh
brew install rbenv
rbenv global 3.1.2 # 해당 글에서는 3.1.2 를 기준으로 진행합니다.
rbenv rehash # 설치한 Ruby 설치 후 재실행
rbenv global 3.1.2 # 전역 버전 설정
```

이후 jekyll을 로컬에서 실행시키기 위해 터미널에서 아래 명령을 사용하여 의존성이 있는 모듈을 모두 설치한후  
다음 명령어를 사용하여 Jekyll을 실행시킵니다. 
```zsh
bundle # 의존성 모듈 설치
bundle exec jekyll serve # jekyll 실행
```
위 명령어를 실행하고 [localhost:4000](http://localhost:4000)으로 접속하여 확인할 수 있다.

## 기본설정
---
### _config.yml 수정
`_config.yml`파일로 가서 여러가지 설정값들을 고정해주어야 한다. 아래값들이 대표적인 설정값들이다.  
`_config.yml`파일에서 아래에 해당하는 값들을 바꾸어주면된다.

- `title`: 블로그 제목입니다. 좌상단의 아바타 바로 아래 표시됩니다.  
  e.g. `title: DevJinto`
- `tagline`: `title` 아래에 작은 글씨로 작성됩니다.  
  e.g. `tagline: Archive for Dev`
- `description`: 블로그의 주소를 넣으면 됩니다.
  e.g. `url: 'https://j1mmyson.github.io'`
- `url`: 블로그의 주소를 넣어주면 됩니다.
  e.g. `url: 'https://Jintopia.github.io'`
- `avatar`: 대표사진으로 쓰일 이미지 파일경로로 일반적으로 이미지 파일은 `/assets/img/`폴더에 넣어 사용합니다. 
  e.g. `avatar: /assets/img/byungwook.png`
- `timezone`: 자신이 속한 지역의 시간대를 넣으면 됩니다. 
  e.g. `timezone: Asia/Seoul`  

제가 작성한 [_config.yml](https://github.com/Jintopia/Jintopia.github.io/blob/master/_config.yml){:target="_blank"}을 참조하시면 됩니다. `_config.yml`을 수정하면 항상 jekyll을 재구동 해 줍니다.

### 글작성방법
Jekyll은 마크다운 문법으로 글을 작성할 수 있습니다. 마크다운 문법에 대한 정보는 [여기](https://goddaehee.tistory.com/307){:target="_blank"}을 참조하시면 됩니다.  
글을 작성한후 반드시 아래 규칙을 지켜주어야 합니다.  
* 형식 : `yyyy-mm-dd-제목.md` 연,월,일 순으로 넣어줍니다.
* 확장자는 마크다운 확장자인 `.md` 또는 `.markdown`으로 합니다.
* 중간에 공백을 넣지 않습니다. 공백이 필요하면 `-`을 사용합니다.
* 작성한 파일은 `_posts` 디렉토리에 넣습니다.

## 배포
---
### Commit
로컬에서의 테스트가 완료되면 수정한 내용을 Github에 업로드합니다.  
우선 `.gitignore`에 `Gemfile.lock`을 추가합니다. 빌드/배포시에 발생 할 수 있는 문제를 사전에 방지합니다.

```zsh
git add -A
git commit -m "first commit"
git push
```

### 기타설정
`gh-pages` 라는 `branch를` 통하여 배포를 진행해왔으나 `GitHub Actions`로 통합되었다.
![GithubSettings](github-settings.png){:style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px;"}
레포지토리의 `Setting-Pages-Source` 란을 `Github Actions`로 변경해주면 끝이다.

배포 과정을 `Actions`탭에서 확인 가능하며 파란색 체크 표시가 뜨면 배포가 정상적으로 완료된 것이다.
해당결과는 `[Github-UserName].github.io` 에서 확인 가능하다.  
![GithubActions](github-actions.png){:style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px;"}

## 문제해결
---
1. `tools/init.sh`가 정상적으로 진행되지 않는경우  
  * `_posts` 폴더 하위의 파일들 삭제
  * `docs` 폴더 삭제
  * `.github/workflows/pages-deploy.yml.hook`의 확장자를 `pages-deploy.yml`로 변경

1. 이미지가 업로드되지 않는경우  
  * 이미지 경로가 정확한지 확인
  * `_config.yml`의 `img_cdn`을 공란으로 만들기

1. deploy 과정에서의 ruby 버전 문제 오류
  * Jekyll 4.3.0 이 ruby 3.2.0 을 사용하는 데 deploy 오류가 있다고 한다 [참조](https://github.com/jekyll/jekyll/issues/9231){:target="_blank"}
  * `jekyll-theme-chirpy.gemspec` 의  `spec.required_ruby_version = [">= 2.5", "< 3.2"]` 로 변경한다.

## 참고
---
* 깃헙 블로그 만들기 : <https://j1mmyson.github.io/posts/StartingBlog/#usage>{:target="_blank"}
* chirpy theme github : <https://github.com/cotes2020/jekyll-theme-chirpy>{:target="_blank"}