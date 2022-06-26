# React기초  


## 목차

1. [React란?](#react란)
2. [실습환경 구축](#실습환경-구축)
3. [react 배포](#react-배포)
4. [컴포넌트 만들기](#컴포넌트-만들기)
5. [Props](#props)
6. [이벤트](#이벤트)  
7. [Create](#create)
8. [Update](#update)
9. [Delete](#delete)


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


## 이벤트
* 컴포넌트에서 이벤트를 발생시키려면 onChangeMode를 사용자정의 태그에 선언한다.

![Header태그](https://github.com/JaeyeongPark/TIL/blob/main/React/img/Header%ED%83%9C%EA%B7%B8.PNG)

* 컴포넌트에서 onClick이벤트를 발생시킨다.

![Header온클릭](https://github.com/JaeyeongPark/TIL/blob/main/React/img/Header%EC%98%A8%ED%81%B4%EB%A6%AD.PNG)

* WEB을 클릭했을 때 이벤트가 발생한다.

![WEB을 클릭](https://github.com/JaeyeongPark/TIL/blob/main/React/img/WEB%EC%9D%84%20%ED%81%B4%EB%A6%AD%ED%96%88%EC%9D%84%20%EB%95%8C.PNG)

* 컴포넌트의 id를 출력하고 싶으면 event.target.id를 사용한다.

![Nav-a태그](https://github.com/JaeyeongPark/TIL/blob/main/React/img/a%ED%83%9C%EA%B7%B8%20id%EA%B0%92.PNG)

* html을 클릭하면 id를 alert를 이용해 출력한다.

![html클릭](https://github.com/JaeyeongPark/TIL/blob/main/React/img/html%EC%9D%84%20%ED%81%B4%EB%A6%AD%ED%96%88%EC%9D%84%20%EB%95%8C.PNG)  


## State
* state는 컴포넌트 렌더링 결과물에 영향을 주는 데이터를 갖고 있는 객체이다.
* Props와 다른 점은 Props는 매개변수처럼 전달되는 반면 state는 컴포넌트 안에서 관리된다.

## State 사용방법
* state를 사용하기 위해서 useState를 import한다.

![useState](https://github.com/JaeyeongPark/TIL/blob/main/React/img/useState.PNG)  
*state를 선언하는 방법은 다음과 같다.

![state선언](https://github.com/JaeyeongPark/TIL/blob/main/React/img/state%EC%84%A0%EC%96%B8.PNG)
*이벤트가 발생할 때 state변수를 변경한다.

![setMode](https://github.com/JaeyeongPark/TIL/blob/main/React/img/setState.PNG)
* state를 이용해서 mode변수의 값이 바뀌면 사용자 태그를 변경하는 코드

![state변경](https://github.com/JaeyeongPark/TIL/blob/main/React/img/state%EB%B3%80%EA%B2%BD.PNG)

## Create
* Create태그를 만들기 위한 a태그를 선언한다.

![a태그(create)](https://github.com/JaeyeongPark/TIL/blob/main/React/img/a%ED%83%9C%EA%B7%B8(Create).PNG)

* Create 컴포넌트를 정의 한다.
* form태그를 이용해 title, body의 데이터를 보내고 props를 사용하여 값을 전달한다.

![Create컴포넌트선언](https://github.com/JaeyeongPark/TIL/blob/main/React/img/Create%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%84%A0%EC%96%B8.PNG)

* newTopic에 새로운 객체를 받는다
* newTopics에는 현재의 topics를 저장한다.
* newTopics에 newTopic을 추가한다.
* setTopics에 newTopics를 넣고 페이지를 새롭게 렌더링한다.

![Create컴포넌트](https://github.com/JaeyeongPark/TIL/blob/main/React/img/Create%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8.PNG)

* Create를 이용하여 새로운 링크를 만들고 내용을 출력할 수 있다.

![Create결과화면](https://github.com/JaeyeongPark/TIL/blob/main/React/img/Create%EA%B2%B0%EA%B3%BC%ED%99%94%EB%A9%B4.PNG)

## Update

* Update는 Create와 대부분 유사하지만 title과 body를 state를 이용해서 관리하는 것이 중요하다.
* state를 설정하지 않으면 기존의 값이 고정되어있어 변경할 수 없다.
* 값이 변경되면 setTitle, setBody를 이용하고 onChange를 이용하여 이벤트를 발생시킨다.

![Update컴포넌트](https://github.com/JaeyeongPark/TIL/blob/main/React/img/Update%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8.PNG)

* Update 버튼을 클릭해서 mode가 Update로 바뀌면 현재 선택한 id와 일치하는 topics의 title과 body를 가져온다.
* 기존 토픽에서 아이디가 같은 부분의 title과 body를 변경하고 setTopics를 이용해 수정한다.

![Update로직](https://github.com/JaeyeongPark/TIL/blob/main/React/img/Update%EB%A1%9C%EC%A7%81.PNG)

## Delete

* Delete는 버튼을 클릭했을 때 해당 부분을 공백으로 만들어주면 쉽게 구현할 수 있다.

![Delete](https://github.com/JaeyeongPark/TIL/blob/main/React/img/Delete.PNG)



## 출처
[생활코딩 React 강의](https://www.youtube.com/watch?v=AoMv0SIjZL8&list=PLuHgQVnccGMCOGstdDZvH41x0Vtvwyxu7&index=1)
