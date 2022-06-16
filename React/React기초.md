# React기초

## 목차

1. [React란?](#react란)
2. [실습환경 구축](#실습환경-구축)
3. [react 배포](#react-배포)
4. [컴포넌트 만들기](#컴포넌트-만들기)
5. [Props](#props)


## React란?
* 사용자 인터페이스를 만들기 위한 JavaScript 라이브러리다.
* React의 핵심적인 역할은 사용자 정의 태그를 만드는 것이다.

## 실습환경 구축
1. [node.js](https://nodejs.org/en/)를 설치한다.
2. Visual Studio Code를 열고 바탕화면에 react-app폴더를 만든다.
3. 터미널을 열고 **npx create-react-app .** 을 입력한다. 
![react설치](https://github.com/JaeyeongPark/TIL/blob/main/React/img/react%20%EC%84%A4%EC%B9%98.PNG))
4. npm start를 입력하면 sample react 화면을 볼 수 있다.

     ![sample react](https://github.com/JaeyeongPark/TIL/blob/main/React/img/sample%20react.PNG)


## react 폴더 구조
* **/src/index.js**

![index.js](https://github.com/JaeyeongPark/TIL/blob/main/React/img/index.PNG)
1. 4번째 줄 import App from './App'; 은 App.js를 import한 것
2. 9번째 줄 <App />은 import한 App.js를 화면에 표시함

* **/src/App.js**

![app.js](https://github.com/JaeyeongPark/TIL/blob/main/React/img/appjs.PNG)


## react 배포
* 터미널에 npm run build를 입력하면 build 폴더가 만들어진다.
* npx serve -s build를 입력하면 사용자에게 index.html을 서비스해준다.

## 컴포넌트 만들기
* 컴포넌트 만들기 전

![before](https://github.com/JaeyeongPark/TIL/blob/main/React/img/%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%20%EB%A7%8C%EB%93%A4%EA%B8%B0%EC%A0%84.PNG)
* 컴포넌트 만든 후

![After](https://github.com/JaeyeongPark/TIL/blob/main/React/img/%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%20%EC%9E%91%EC%84%B1.PNG)

* 컴포넌트를 만들때는 첫번째 글자를 대문자로 작성한다.

## Props
* react에서 속성을 prop이라고 한다.
* 사용자 정의 태그에 속성을 주고 컴포넌트에서 props를 이용해 받을 수 있다.
* App에서 사용자 정의 태그에 속성을 지정해준다.

![props-app](https://github.com/JaeyeongPark/TIL/blob/main/React/img/props-app.PNG)
* Header에서 {props.title}을 이용해서 title에 저장된 REACT를 나타낼 수 있다.

![props-Header](https://github.com/JaeyeongPark/TIL/blob/main/React/img/props-Header.PNG)
* 브라우저에서 props를 보면 객체안에 title: "REACT"가 들어가있다.

![props-log](https://github.com/JaeyeongPark/TIL/blob/main/React/img/props-log.PNG)

* 객체를 배열로 선언해서 리스트를 만들 수 있다.
* topics의 배열에 저장된 객체의 수만큼 for문을 돌린다.
* li 태그들을 구분하기 위한 key값으로 각각 다른 값을 가지고 있는 t.id를 대입한다.
* title에 저장된 값들로 리스트에 표시한다.

![props-Nav](https://github.com/JaeyeongPark/TIL/blob/main/React/img/props-Nav.PNG)
* props를  결과 화면

![props-결과 화면](https://github.com/JaeyeongPark/TIL/blob/main/React/img/props-%EA%B2%B0%EA%B3%BC%ED%99%94%EB%A9%B4.PNG)







## 출처
[생활코딩 React 강의](https://www.youtube.com/watch?v=AoMv0SIjZL8&list=PLuHgQVnccGMCOGstdDZvH41x0Vtvwyxu7&index=1)
