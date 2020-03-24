---
title: "Tech"
date: 2020-03-24T23:03:00+09:00
---

# MacOS에서 Hugo + github 설정

## 1. Hugo, git설치

homebrew를 이용하여 설치를 진행함

``` #> brew install hugo ```

``` #> brew install git ```

<br> </br> 

## 2. github repository 생성

생성시 Repository name에 Owner명 + github.io 라고 입력하면 바로 접근이 가능함

> 예시) Owner: borys-dad, Repository name: borys-dad.github.io

repository는 hugo의 컨텐츠를 저장할 저장소 하나, hugo의 웹사이트 버전을 저장하는 용 Owner.github.io가 필요함

저장소용 repository를 remote로 설정하고 github.io를 submodule로 해야함

<br> </br>

## 3. Hugo 저장소 생성

``` #> hugo new site 폴더명 ```  나는 폴더명을 blog로 설정하였음

> #> hugo new site blog



<br> </br>

## 4. Hugo Theme 다운로드

<https://themes.gohugo.io/> 여기로 가서 마음에 드는 Hugo theme를 고른다.

마음에 드는 테마가 있는 경우 download를 클릭하여 해당 테마의 github 페이지에서 clone download 링크 복사

``` #> cd blog ```  아까 hugo 저장소로 만들었던 blog 폴더로 진입

``` #> cd themes ``` 

``` #> git clone 복사한 테마주소 ```

> #> git clone https://github.com/zzossig/hugo-theme-zzo.git

<br> </br>

## 5. config.toml 설정

다운로드 받은 테마의 설정은 hugo 저장소를 생성한 blog 폴더내에 config.toml에서 진행한다.

themes 폴더 안에 받은 테마폴더를 기재하면 되며 테마마다 config.toml을 지원하는 내용이 다르니

테마를 다운로드 받은 페이지에서 샘플을 보거나 테마안에 exampleSite 폴더를 참조하자

<br> </br>

## 6. Hugo 구동 후 확인

``` #> hugo server -D ```  서버구동

서버 구동 후 브라우져에서 localhost:1313 으로 접속하여 페이지가 나오는지 확인하면 된다

<br> </br>

## 7. Repository 설정

github에서 생성한 2개의 repository를 설정해보자. 먼저 hugo 저장소인 blog 폴더로 이동

``` #> git init ```

``` #> git remote add origin 내 깃헙 레포 주소 ```

> #> git remote add origin https://github.com/borys-dad/blog.git

``` #> git submodule add -b master 내 깃헙.io 주소 public ```

> #> git submodule add -b master https://github.com/borys-dad/borys-dad.github.io.git public

<br> </br> 

## 8. 컨텐츠 업로드

Hugo 저장소인 blog 폴더로 이동

``` #> hugo -t 테마명 ``` 테마가 적용된 블로그 내용을 public에 생성

``` #> cd public ```

``` #> git add .  ``` 수정된 파일을 index로 올림

``` #> git commit -m "msg" ``` 변경내용 기재

``` #> git push origin master ``` commit을 borys-dad.github.io에 push

``` #> cd .. ``` blog 저장소에도 동일하게 적용

``` #> git add . ```

``` #> git commit -m "msg" ```

``` #> git push origin master ```

위의 내용을 항사 반영하기 힘드니 아래의 내용을 복사해서 shell script로 자동화 시키자

``` 
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project.
hugo -t hugo-theme-geppaku

# Go To Public folder
cd public
# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back up to the Project Root
cd ..


# blog 저장소 Commit & Push
git add .

msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

git push origin master

```

<br> </br>

## 9. 댓글 plugin 추가하기

나는 댓글창으로 라이브리(live-re)를 붙여놨다. 이유는 카카오톡, 네이버 등과 연동시킬수 있어서

이런걸 원치 않는다면 disqus나 Utterance 같은 댓글 플러그인을 사용해도 괜찮을 것 같다. 