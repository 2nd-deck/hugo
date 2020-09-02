---
title: Book - 실전 리액트 프로그래밍 / 이재승
date: 2020-09-06
categories: ["No.1 Hold"]
---

실전 리액트 프로그래밍 - 이재승

## 기본정보

*   프로그래밍 인사이트 2019

## 리액트 프로젝트 시작하기
1. createElement 구조
    - React.createElement(component, props, ...children) => ReactElement
        - component는 일반적으로 문자열이나 리액트 컴포넌트, component의 인수가 문자열이면 HTML 태그에 해당하는 돔 요소가 생성.
        - Props는 컴포넌트가 사용하는 데이터. 돔 요소의 경우 style, className등의 데이터가 사용될 수 있다.
        - children은 해당 컴포넌트가 감싸고 있는 내부의 컴포넌트를 가리킨다.
    - 대부분의 리액트 개발자는 createElement를 직접 작성하지 않는다. 일반적으로 바벨(babel)의 도움을 받아서 JSX 문법을 사용.
2. babel
    - 바벨은 자바스크립트 코드를 변환해 주는 컴파일러
    - 바벨을 사용하면 최신 자바스크립트 문법을 지원하지 않는 환경에서도 최신 문법 사용가능
    - 코드에서 주석을 제거하거나 코드를 압축하는 용도로도 사용
    - 리액트에서는 JSX 문법을 사용하기 위해 바벨을 사용
```
npm install @babel/cli @babel/preset-react
```
    - @babel/cli 에는 커맨드 라인에서 바벨을 실행할 수 있는 바이너리 파일 포함
    - @babel/preset-react(리액트 애플리케이션을 만들때 필요한 플러그인을 모아놓은 프리셋)에는 JSX로 작성된 코드를 createElement 함수를 이용한 코드로 변환 해주는 바벨 플러그인 포함
```
npx babel --watch src --out-dir . --presets @babel/preset-react
```
    - npx 명령어는 외부 패키지에 포함된 실행 파일을 실행할 때 사용된다.
    - 외부 패키지의 실행 파일은 ./node_modules/.bin/ 밑에 저장되며 npx babel은 ./node_modules/.bin/babel을 입력하는 것과 비슷
    - src 폴더에 있는 모든 자바스크립트 파일을 @babel/preset-react 프리셋을 이용해서 변환 후 현재 폴더에 같은 이름의 자바스크립트 파일을 생성한다.
    - watch 모드로 실행하면 src 폴더의 자바스크립트 파일을 수정할 때마다 자동으로 변환 후 저장한다.
3. webpack
    - 웹팩(webpack)은 자바스크립트로 만든 프로그램을 배포하기 좋은 형태로 묶어주는 툴
    - 웹팩은 ESM(ES6의 모듈 시스템)과 commonJS를 모두 지원한다. 이들 모듈 시스템을 이용해서 코드를 작성하고 웹팩을 실행하면 예전 버전의 브라우저에서도 동작하는 자바스크립트 코드를 만들 수 있다.
```
// file1.js 파일
export default function func1(){}
export function func2() {}
export const variable1 = 123;
export let variable2 = 'hello';

//file2.js 파일
import myFunc1, { func2, variable1, variable2 } from './file1.js';

//file3.js 파일
import { func2 as myFunc2 } from './file1.js';
```
    - ESM 문법을 익히기 위한 모듈을 내보내고 가져오는 코드
    - default 키워드는 한 파일에서 한 번만 사용 가능하며 default로 내보내진 코드는 괄호 없이 가져올 수 있고, 이름은 원하는 대로 정할 수 있다.
    - default 키워드 없이 내보내진 코드는 괄호를 사용해서 가져오고, 가져오는 이름은 내보낼때 사용된 이름을 그대로 가져와야 한다.
```
npm init -y
```
    - 명령어를 실행하면 package.json 파일이 생성
```
npm install webpack webpack-cli react react-dom
```
    - 외부 패키지 설치(웹팩, 리액트 패키지)
    - 리액트 패키지에는 react.production.min.js와 react.development.js 파일이 포함
    - react-dom 패키지에는 react-dom.production.min.js와 react-dom.development.js 파일이 포함
    - npx webpack 웹팩 실행

4. 클래스형 컴포넌트와 함수형 컴포넌트
    - 기능적인 측면에서 클래스형 컴포넌트는 함수형 컴포넌트가 할 수 있는 모든 일을 할 수 있다.
    - 리액트 16.8 이전 버전의 함수형 컴포넌트는 상탯값을 가질 수 없고 리액트 컴포넌트의 생명 주기 함수를 작성할 수 없다.
    - 리액트 16.8부터 훅(hook)이라는 기능이 추가되면서 함수형 컴포넌트에서도 상탯값과 생명 주기 함수 코드 작성 가능.

5. create-react-app
    - 리액트로 웹 애플리케이션을 만들기 위한 환경을 제공
    - 바벨, 웹팩, 테스트 시스템, HMR, ES6+문법, CSS 후처리등 거의 필수라 할 수 있는 개발 환경도 구축
```
npx create-react-app cra-test
```
또는
```
npm install -g create-react-app
create-react-app cra-test
```
```
npm start
```
    - HMR : 변경된 파일이 바로 적용 
    - npm start는 개발 모드에서 동작
    - index.html, index.js파일은 빌드 시 예약된 파일 이름으로 지우면 안된다.
    - index.js로부터 연결된 모든 자바스크립트 파일과 CSS파일은 src 폴더 밑에 있어야 한다.
    - serviceWorker.js 파일에는 PWA(progressive web app)와 관련된 코드가 들어있다. PWA는 오프라인에서도 잘 동작하는 웹 애플리케이션을 만들기 위한 기술
    - PWA 기능을 원하면 index.js 파일에 serviceWorker.register(); 코드를 넣으면 된다.

6. create-react-app 주요 명령어
    - npm start 
        + 개발모드로 프로그램 실행. 
        + HMR이 동작하므로 코드 수정시 즉시 반영. 
        + API 호출을 위해 https로 실행할때 
        ```
        set HTTPS=true && npm start
        ```
        + 자체 서명된 인증서와 함꼐 https 사이트로 접속
    - npm run build
        + 배포환경에서 사용할 파일을 생성
    - npx serve -s build
        + serve 패키지는 노드(node.js) 환경에서 동작하는 웹 서버 애플리케이션
        + 정적 파일을 서비스할 때 사용
        + build/static 폴더 밑에 생성된 파일이 이름에 해시값이 포함되어 새로 빌드를 하더라도 변경되지 않은 파일은 브라우저에 캐싱되어 있는 파일을 사용. 따라서 재방문의 경우 빠르게 페이지가 렌더링
        + 모든 CSS파일은 build/static/css/main.{해시값}.chunk.css 에 저장
        + import 키워드를 이용해 가져온 폰트,이미지등의 리소스 파일은 build/static/media 폴더 밑에 저장
    - npm test
        + 테스트 코드가 실행
        + 제스트(jest)라는 테스트 프레임워크를 기반
        + create-react-app으로 프로젝트를 생성하면 App.test.js 파일이 생성된다.
        + 다음 조건을 만족하면 테스트 파일로 인식   
        ```
        __tests__ 폴더 밑에 있는 모든 자바스트립트 파일
        파일 이름이 .test.js로 끝나는 파일
        파일 이름이 .spec.js로 끝나는 파일
        ```
    - npm run eject
        + 내부 설정 파일이 밖으로 노출
        + 이 기능으로 바벨이나 웹팩의 설정을 변경
    - npm install core-js
        + core-js 패키지를 이용한 폴리필
7. CSS
    - css-module을 사용하면 일반적인 CSS 파일에서 클래스명 충돌을 피할 수 있다.
    - {이름}.module.css 로 파일을 생서하면 css-module이 된다.
    - Sass는 CSS와 비슷하지만 별도의 문법을 이용해서 생산성이 높은 스타일 코드를 작성할 수 있게 한다.
    - Sass 문법에 있는 변수, 믹스인(mixin)등의 개념을 이용하면 스타일 코드를 재사용
    - create-react-app에서 Sass를 사용하고 싶다면 다음 패키지를 설치
    ```
    npm install node-sass
    ```
8. SPA(Single Page Application)
    - SPA는 최초 요청시 서버에서 첫 페이지를 처리하고 이후의 라우팅은 클라이언트에서 처리하는 웹 애플리케이션
    - SPA 구현을 위해 두 가지 기능이 필요
        + 자바스크립트에서 브라우저로 페이지 전환 요청을 보낼수 있다. 단 브라우저는 서버로 요청을 보내지 않아야 한다.
        + 브라우저의 뒤로 가기와 같은 사용자의 페이지 전환 요청을 자바스크립트에서 처리할 수 있다. 이떄도 브라우저는 서버로 요청을 보내지 않아야 한다.
    - 이러한 조건을 만족하는 브라우저 API는 pushState, replaceState 함수와 popstate 이벤트이다.
    - replaceState 함수는 pushState와 거으 ㅣ같지만 스택에 state를 쌓지 않고 가장 최신의 state를 대체한다.
    - 브라우저 히스토리 API를 이용해서 페이지 라우팅 처리를 직접 구현할 수도 있지만 react-router-dom을 사용하면 도움이 된다.
    ```
    npm install react-router-dom
    ```
    - 웹을 위한 react-router 패키지
    - 같은 path 속성값을 갖는 Route 컴포넌트를 여러 번 작성해도 된다.
    - Route를 통해 렌더링되는 컴포넌트는 match라는 속성값을 사용할수 있다.
    - match.url은 Route 컴포넌트의 path 속성값과 같다.
    - Route 컴포넌트의 path 속성값에서 콜론을 사용하면 파라미터를 나타낼수 있다.
    - 추출된 파라미터는 match.params.{파라미터이름} 형식으로 사용될 수 있다.

## ES6+를 품은 자바스크립트
### 변수를 정의하는 새로운 방법: const, let
1. var가 가진 문제
    - 함수 scope 문제: var로 정의된 변수의 정의된 위치에 의해 scope이 결정된다. 정의된 함수 밖에서 사용하면 에러 발생. 또는 반복문에 사용된 i가 반복문이 끝난 이후에도 계속 남게 되는 문제점.
    - hoisting: var로 정의된 변수는 그 변수가 속한 scope의 최상단으로 끌어올려진다. 변수의 정의만 끌어올려지고 값은 원래 정의했던 위치에서 할당된다.
2. var의 문제를 해결하는 const, let
    - const와 let은 블록 스코프
    - 블록 스코프는 블록을 벗어나면 변수를 사용할 수 없다.
    - const는 변수를 재할당 불가능하게 만든다.
### 객체와 배열을 간편하게 생성/수정
1. 단축 속성명
    - 새로 만들려는 객체의 속성값 일부가 이미 변수로 존재하면 간단하게 변수 이름만 작성
    - 속성값이 함수이면 function 키워드 없이 함수명만 
2. 계산된 속성명


    

