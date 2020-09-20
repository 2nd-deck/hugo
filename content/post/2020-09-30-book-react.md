---
title: Book - 실전 리액트 프로그래밍 / 이재승
date: 2020-09-30
categories: ["No.1 Hold"]
---

실전 리액트 프로그래밍 - 이재승

## 기본정보

*   프로그래밍 인사이트 2019

## 감상
자바스크립트 경험이 거의 없고 생활코딩의 리액트 강좌만 들은 상태에서, 이책은 잘못된 선택이다. 기본지식이 부족한 것도 문제이지만 정리되지 않은 문장과 예문이라는 느낌이 강하게 든다. 자신이 아는 것과 그것을 다른이에게 가르치는 것은 서로 다른 문제이다. 또한 글쓰기는 또다른 문제이다. 한페이지를 읽고 넘어 가는데 너무 시간이 많이 걸리고 그 내용을 정리하려면 문장을 분해해서 다시 조합하여 정리해야한다. 말이 너무 어려워 끝내 책의 순서는 그대로 따라가되 내용은 검색하여 친절한 블로그의 도움을 받았다.       
이 모든 문제는 나의 기본지식이 부족해서 그럴 것이다.    

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
2. 전개 연산자
```
const numbers = [1, 3, 7, 9];
Math.max(...numbers);
```
    - 전개 연산자는 배열이나 객체의 모든 속성을 풀어놓을때 사용하는 문법
    - 전개 연산자를 사용하면 동적으로 함수의 매개변수를 전달할 수 있다.
```
[1, ...[2, 3], 4];  //[1, 2, 3, 4]
```
    - 배열 리터럴에서 중간에 전개 연산자를 사용하면 전개 연산자 전후의 순서가 유지
    - Date 생성자의 매개변수 순서대로 날짜 데이터를 관리하면 Date 객체를 쉽게 생성 가능
3. 배열 비구조화
    - 배열의 여러 속성값을 변수로 쉽게 할당
```
const arr = [1, 2];
const [a, b] = arr;
console.log(a); // 1
console.log(b); // 2
```
```
let a, b;
[a, b] = [1, 2];
```
4. 객체 비구조화
    - 객체의 여러 속성값을 변수로 쉽게 할당할 수 있는 문법
```
const obj = { age: 21, name: 'mike'};
const {age, name} = obj;
consol.log(age);  // 21
consol.log(name);  // mike
```
    - 객체 비구조화에서는 중괄호 사용
    - 배열 비구조화에서는 배열의 순서가 중요, 객체 비구조화에서 순서는 무의미
5. 매개변수 기본값
```
function printLog(a = 1){
    console.log({a});
}
printLog();  // {a: 1}
```
    - 인수 없이 함수를 호출하므로 a에는 undefined가 입력된다. 기본값이 정의된 매개변수에 undefined를 입력하면 정의된 기본값 1이 사용된다.
6. 나머지 매개변수
```
function printLog(a, ...rest){
    console.log({a, rest});
}
printLog(1, 2, 3);  // { a: 1, rest: [2, 3]}
```
    -하나의 인자를 제외한 나머지를 rest 매개변수에 할당
7. 명명된 매개변수
```
const numbers = [10, 20, 30, 40];
const result1 = getValues(numbers, 5, 25);
const result2 = getValues({numbers, greaterThan: 5, lessThan: 25});
```
    - result1의 경우 매개변수의 이름이 보이지 않아 인수가 의미하는 바를 알기 어렵다
    - result2처럼 명명된 매개변수를 이용하면 매개변수의 이름이 노출된다.
8. 화살표 함수
    - ES6에서는 화살표 함수를 이용해 함수를 정의하는 방법이 추가되었다.
```
const add = (a, b) => a + b;
console.log(add(1, 2));  // 3
const add5 = a => a + 5;
console.log(add5(1));  //6
const addAndReturnObject = (a, b) => ({result: a + b});
console.log(addAndReturnObject(1, 2).result); //3
```
    - 화살표 함수를 중괄호를 감싸지 않으면 오른쪽의 계산 결과가 반환(return 키워드 생략 가능)
    - 매개변수가 하나라면 매겨변수를 감싸는 소괄호 생략 가능
    - 객체를 반환해야 한다면 소괄호로 감싸야 함.
```
const add = (a, b) => {
    if (a <= 0 || b <= 0 ) {
        throw new Error ('must be positive number');
    }
    return a + b;
}
```
    - 화살표 함수에 여러줄의 코드가 필요하다면 중괄호로 묶고, 반환값에는 return 키워드 사용
    - this와 arguments가 바인딩되지 않는다.
9. promise
    - 프로미스(promise)는 비동기 상태를 값으로 다룰 수 있는 객체
    - 자바스크립트에서 비동기 프로그래밍의 한 가지 방식으로 콜백(callback) 패턴을 많이 사용하나, 콜배깅 조금만 중첩돼도 코드가 상당히 복잡해지는 단점이 있다.
    - 프로미스를 사용하면 비동기 프로그래밍을 할 때 코드를 순차적으로 작성할 수 있다.
    - 프로미스의 세 가지 상태
        + 대기 중(pending): 결과를 기다리는 중
        + 이행됨(fulfilled): 수행이 정상적으로 끝났고 결과값을 갖고 있음.
        + 거부됨(rejected): 수행이 비정상적으로 끝남
        + settle:수행된 상태(성공 또는 실패)
```
const p1 = new Promise((resolve, reject) => {

});
const p2 = Promise.reject('error message');
const p3 = Promise.resolve(param);
```
    - new 키워드를 사용해서 프로미스를 생성. 이때 대기 중 상태가 된다.
    - new 키워드를 사용하지 않고 Promise.reject를 호출하면 거부됨 상태인 프로미스가 생성
    - Promise.resolve를 호출해도 프로미스가 생성.
```
requestData().then(onResolve, onReject);
Promise.resolve(123).then(data => console.log(data));
Promise.reject('err').then(null, error => console.log(error));
```
    - then은 처리됨 상태가 된 프로미스를 처리할 떄 사용되는 메서드
    - catch는 프로미스 수행 중 발생한 예외를 처리하는 메서드. then 메서드의 onReject 함수와 같은 역할
    - finally는 프로미스가 이행됨 또는 거부됨 상태일 때 호출되는 메서드
    - promise.all 병렬로 처리
    - promise.race 여러 개의 프로미스 중에서 가장 빨리 처리된 프로미스를 반환
10. promise 2
    - 동기식 처리 모델: 직렬적으로 task를 수행. 순차적으로 실행되므로 어떤 작업이 수행 중이면 다음 task는 대기
    - 비동기식 처리 모델: 병렬적으로 task를 수행. task가 종료되지 않은 상태라 하더라도 대기하지 않고 즉시 다음 task를 실행
    - 자바스크립트의 대부분의 DOM 이벤트와 Timer함수, Ajax 요청은 비동기식 처리 모델로 동작한다.
    - 자바스크립트는 요청을 병렬로 처리하여 다른 요청이 블로킹 되지 않는 장점이 있다.
    - 비동기 처리를 위해 콜백 패턴을 사용하면 처리 순서를 보장하기 위해 여러 개의 콜백 함수가 네스팅(nesting, 중첩)되어 복잡도가 높아지는 콜백 헬이 발생하는 단점이 있다. 가독성을 나쁘게 하며 실수를 유발.

### 리액트 개념
1. 상탯값과 속성값으로 관리하는 UI 데이터
    - UI 데이터는 컴포넌트 내부에서 관리되는 상태값(state)과 부모 컴포넌트에서 내려 주는 속성값(props)으로 구성
    - 리액트는 화면을 그리는 모든 코드는 컴포넌트의 렌더(render) 함수로 작성. UI 데이터가 변경되면 리액트가 렌터 함수를 이용해서 화면을 자동으로 갱신해 주며, 이것이 리액트의 가장 중요한 역할
    - 상태값을 변경해주는 setState 메서드는 비동기로 동작
2. 리액트 요소와 가상 돔
    - 리액트는 렌더링 성능을 위해 가상 돔을 활용. 메모리에 가상 돔을 올려 놓고 이전과 이후의 가상 돔을 비교하여 변경된 부분만 실제 돔에 반영
    - 리액트에서 데이터 변경에 의한 화면 업데이트는 렌더 단계와 커밋 단계를 거친다.
    - 렌더 단계는 실제 돔에 반영할 변경 사항을 파악하는 단계이고, 커밋 단계는 파악된 변경 사항을 실제 돔에 반영하는 단계
3. 생명 주기 메서드
    - 모든 컴포넌트는 다음과 같이 세 단계를 거친다. 초기화 단계, 업데이트 단계, 소멸 단계
    - 각 단계 속에서 호출되는 메서드를 생명 주기 메서드라고 부른다.   
    - ![method](/img/react_03_01.jpg)
    - 렌더링 시 예외가 발생하면 호출되는 메서드
        + static getDerivedStateFromErro()
        + componentDidCatch()
    - constructor 메서드
    - ```
    constructor(props) {
        super(props);
        this.state = {
            currentMovie: props.age < 10 ? '뽀로로' : '어벤져스',
        };
    }
    ```
        + constructor 메서드 내부에서 반드시 super 함수를 호출해야 한다.
        + 상태값을 직접 할당하는 것은 constructor 메서드에서만 허용
        + constructor 메서드 내부에서 호출되는 setState 메서드는 무시된다. setState 메서드 호출은 컴포넌트가 마운트된 이후에만 유효
    - getDerivedStateFromProps 메서드
        + 속성값을 이용해서 새로운 상태값을 만들 때 사용되며 render 메서드가 호출되기 직전에 호출된다.
        + static getDerivedStateFromProps (props, state)
        + 정적 메서드이기 떄문에 함수 내부에서 this객체에 접근할 수 없다.
    - render 메서드
        + 컴포넌트를 정의할 때 화면에 보여질 반환값의 내용을 결정
        + 배열을 반환할 떄 각 리액트 요소는 key 속성값을 갖고 있어야 한다.
        + 리액트 프래그먼트<React.Fragment>를 사용하면 내부의 리액트 요소에 key속성값을 부여하지 않아도 된다.
        + null 또는 bool을 반환하면 아무것도 렌더링하지 않는다.
        + 리액트 포털을 사용하면 컴포넌트의 현재 위치와는 상관없이 특정 돔 요소에 렌더링할 수 있다
    - componentDidMount
        + render 메서드의 첫 번째 반환값이 실제 돔에 반영된 직후 호출된다.
        + render 메서드에서 반환한 리액트 요소가 돔에 반영되어야 알수 있는 값을 얻을 수 있다.
    - shouldComponentUpdate 메서드
        + 성능 최적화를 위해 존재
        + shouldComponentUpdate(nestProps, nextState)
        + 불 타입을 반환 한다. True를 반환하면 render 메서드가 호출
        + 변수 비교를 통해 render 메서드를 호출할지 결정하므로 성능과 관련있다.
    - getSnapshotBeforeUpdate 메서드
        + 렌더링 결과가 실제 돔에 반영되기 직전에 호출
        + 호출 되는 시점에 이전 돔 요소의 상태값을 가져오기 좋다
    - componentDidUpdate 메서드
        + 업데이트 단계에서 마지막으로 호출되는 생명 주기 메서드
        + componentDidUpdate(prevProps, prevState, snapshot)
        + 가상 돔이 실제 돔에 반영된 후 호출
        + 새로 반영된 돔의 상태값을 가장 빠르게 가져올 수 있는 메서드
        + 속성값이나 상태값이 변경된 경우 API를 호출 하는 용도로 사용되기도 한다.
    - componentWillUnmount 메서드
        + 소멸 단계에서 호출되는 유일한 생명 주기 메서드
        + 끝나지 않은 네트워크 요청을 취소, 타이머 해제, 구독 해제 등의 작업을 처리하기 좋다.
    - getDerivedStateFromError, componentDidCatch 메서드
        + 생명 주기 메서드에서 예외가 발생하면 getDerivedStateFromError, componentDidCatch 메서드를 구현한 가장 가까운 부모 컴포넌트를 찾는다.
        + getDerivedStateFromError(error) 에러 정보를 상태값에 저장해서 화면에 나타내는 용도
        + componentDidCatch(error, info) 에러 정보를 서버로 전송하는 용도
4. 콘텍스트 API로 데이터 전달하기
    - 상위 컴포넌트에서 하위 컴포넌트로 데이터를 전달할 때 속성값이 사용되는데 많은 수의 하위 컴포넌트로 전달할 때에는 속성값을 내려주는 코드를 반복적으로 작성해야 하는 문제가 있다.
    - 콘텍스트 API를 사용하면 컴포넌트 중첩 구조가 복잡한 상황에서도 비교적 쉽게 데이터를 전달할 수 있다.
    - React.createContext(defaultValue) => {Provider, Cosumer}
    - 상위 컴포넌트에서는 Provider 컴포넌트를 이용해서 데이터를 전달
    - 하위 컴포넌트에서는 Cosumer 컴포넌트를 이용해서 데이터를 사용. Consumer컴포넌트는 데이터를 찾기 위해 상위로 올라가면서 가장 가까운 Provider 컴포넌트를 찾는다. 찾지 못하면 기본값을 사용
5. ref 속성값으로 자식 요소에 접근
    - 돔 요소에 직접 접근해야 할때 ref 속성값을 이용하면 자식 요소에 직접 접근할 수 있다.

### 컴포넌트 작성
1. 컴포넌트 파일 작성법
    - 코드를 그룹으로 나누고 우선순위에 따라 배치
        + 속성값 타입 정의 코드
        + 상태값 초기화 코드
        + render 메서드를 제외한 나머지 생명 주기 메서드
        + 생명 주기 메서드를 제외한 나머지 메서드
        + render 메서드
        + 컴포넌트 외부에서 정의하는 변수와 함수
    - 속성값 타입 정의 : prop-types
        + prop-types는 속성값의 타입 정보를 정의할 때 사용하는 리액트 공식 패키지
        + 동적 타입의 언어는 큰 규모의 프로그램을 작성할 때 생산성이 오히려 떨어진다.
        + 컴포넌트 사용 시 속성값에 잘못된 타입이 입력되면 콘솔에 에러 메시지 출력
        ```
        class MyComponent extends React.Component {
            static propTypes = {
                //리액트 요소
                menu: PropTypes.element,

                //렌더 함수가 리턴할 수 있는 모든 것
                description: PropTypes.node,

                //Message 클래스로 생성된 모든 객체
                message: PropTypes.instanceOf(Message),

                //배열에 포함된 값 중에서 하나를 만족
                menu: PropTypes.oneOfType([PropTypes.number, ProTypes.string]),

                //특정 타입만 포함하는 배열
                age: ProTypes.arrayOf(ProTypes.number),

                //객체 속성값 타입 정의
                info: PropTypes.shape({
                    color: proTypes.string,
                    weight: proTypes.number,
                }),

                //객체에서 모든 속성값의 타입이 같은 경우
                infos: PropTypes.objectOf(PropTypes.number),
            };
        }
    - 조건부 렌더링
        ```
        const v1 = 'ab' && 0 && 2;  //v1 === 0
        const v2 = 'ab' && 2 && 3;  //v2 === 3
        const v3 = 'ab' || 0;  //v3 === 'ab'
        const v4 = '' || 0 || 3;  //v4 === 3
        ```
        + &&, || 연산자 모두 마지막으로 검사한 값을 반환
        + && 연산자는 첫 거짓(false) 또는 마지막 값을 반환하고, ||연산자는 첫 참(True) 또는 마지막 값을 반환 한다.
        + 특정 조건을 만족해야 렌더링할 리액트 요소를 && 연산자 끝에 작성하고 앞쪽에는 해당 조건을 작성하는 방식으로 조건부 렌더링을 구현
        + && 연산자를 사용할 때 주의해야 할 점은 변수가 숫자 타입인 경우 0은 거짓이고 문자열 타입인 경우 빈 문자열도 거짓이다.
    - 관심사 분리를 위한 프레젠테이션, 컨테이너 컴포넌트 구분하기
2. 이벤트 처리 함수 작성
