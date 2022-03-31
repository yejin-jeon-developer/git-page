---
title:  "React 기초 정리 2"
excerpt: "React 사용법"
categories:
  - react
---
##React 시작하기
1. 리액트를 작업할 때 webpack 이나 parcel 같은 번들러를 이용해서 작업
2. 리액트 파일은 JSX 문법으로 작성되거나 최신 JS 문법으로 작성되기 때문에, babel 을 사용해서 브라우저 호환성을 생각해야함
3. facebook이 강력한 리액트 개발 도구를 지원 : create-react-app (Node.js 설치 필요)

##Create React App 사용하기
1. Node.js 설치
```
$ brew update
$ brew install node
$ node -v
$ npm -v
```
2. 터미널 실행 후 명령어 입력
```
$ npx create-react-app hello
```
참고사항 : npx란 자바스크립트 패키지 관리 모듈인 npm(Node Package Module)의 5.2.0 버전부터 새로 추가된 도구
3. 리액트 앱 실행
```
$ cd hello
$ npm start
```
