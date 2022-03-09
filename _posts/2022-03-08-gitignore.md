---
title:  ".gitignore 파일 생성"
excerpt: "프로젝트 시작을 위한 gitignore 자동 생성 방법"

categories:
  - git
tags:
  - git
last_modified_at: 2022-03-08T22:06:00-05:00
---

# .gitignore 파일 생성 방법
프로젝트 초기 설정시 필요 없는 파일들을 .gitignore를 각각 지정했었는데, 자동으로 생성해주는 site가 있어 공유 하고자 한다.  

## .gitignore란?

프로젝트 생성 후 개발하며 필요한 source code 이외의 불필요한 빌드 산출물 혹은 ide 설정 파일 등이 생성된다.
.gitignore는 이러한 파일들을 git 관리 대상에서 제외하기 위해(commit에 포함되지 않도록) 규칙들을 지정한 파일이다.

## .gitignore 생성방법
[gitignore.io](http://gitignore.io "Title") 에 접속하여 개발하려는 프로젝트에 맞는 '운영체제, 개발환경(IDE), 프로그래밍 언어' 를 입력 후 생성 한다.
<center><img src="/assets/images/gitignore.jpg" width="100%" height="100%"></center>

  

## 최상위 디렉토리에 저장

gitignore.io에서 생성된 gitignore를 복사하여 vi, 메모장, vim 등을 활용하여 프로젝트 최상위 디렉토리에 파일명 .gitignore로 저장한다.

ex) .gitignore

	# Created by https://www.toptal.com/developers/gitignore/api/macos,android,androidstudio
	# Edit at https://www.toptal.com/developers/gitignore?templates=macos,android,androidstudio

	### Android ###
	# Gradle files
	.gradle/
	build/

	# Local configuration file (sdk path, etc)
	local.properties

	# Log/OS Files
	*.log

	# Android Studio generated files and folders
	captures/
	.externalNativeBuild/
	.cxx/
	*.apk
	output.json

	# IntelliJ
	*.iml
	.idea/
	misc.xml
	deploymentTargetDropDown.xml
	render.experimental.xml
	...


### 추가) .gitignore에서 특정 파일 제외 방법
	# 파일 제외 (파일명.확장자)
	파일명.txt
 
	# 현재 경로에 있는 파일만 제외 (다른 경로의 동일한 파일명은 추적)
	/파일명.txt
 
	# 특정 경로안의 특정 파일 제외
	폴더명/파일명.txt
 
	# 특정 폴더안의 파일 전부 제외
	폴더명/
 
	# 해당 확장자 파일 전체 제외
	*.txt
 
	# 예외
	!제외할 파일명.txt

