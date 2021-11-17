event delegation에 관해 설명해주세요.

**Event Bubbling(이벤트 버블링)**

-   이벤트 버블링은 특정 화면 요소에서 이벤트가 발생했을 때 해당 이벤트가 더 상위의 화면 요소들로 전달되어 가는 특성

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e8ef96ef-fa71-43a5-b5c1-6053ee1107c6/Untitled.png)

```jsx
var divs = document.querySelectorAll("div");
divs.forEach(function (div) {
    div.addEventListener("click", logEvent);
});

function logEvent(event) {
    console.log(event.currentTarget.className);
}
```

**Event Capture(이벤트 캡처)**

-   이벤트 버블링과 반대 방향으로 진행되는 이벤트 전파 방식

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4e7973cb-b019-4b4d-bd7e-c228b4843944/Untitled.png)

```jsx
var divs = document.querySelectorAll("div");
divs.forEach(function (div) {
    div.addEventListener("click", logEvent, {
        capture: true, // default 값은 false입니다.
    });
});

function logEvent(event) {
    console.log(event.currentTarget.className);
}
```

`capture:true`를 설정해주면 됩니다. 그러면 해당 이벤트를 감지하기 위해 이벤트 버블링과 반대 방향으로 탐색

event.stopPropagation()을 사용해 화면 요소의 이벤트만 사용

**이벤트 위임 - Event Delegation**

-   이벤트 위임을 한 문장으로 요약해보면 ‘하위 요소에 각각 이벤트를 붙이지 않고 상위 요소에서 하위 요소의 이벤트들을 제어하는 방식’

```jsx
<h1>오늘의 할 일</h1>
<ul class="itemList">
	<li>
		<input type="checkbox" id="item1">
		<label for="item1">이벤트 버블링 학습</label>
	</li>
	<li>
		<input type="checkbox" id="item2">
		<label for="item2">이벤트 캡쳐 학습</label>
	</li>
</ul>

var itemList = document.querySelector('.itemList');
itemList.addEventListener('click', function(event) {
	alert('clicked');
});
```

리스트 아이템이 추가하더라도 추가로 이벤트 리스너를 등록하지 않아도 된다.

`**this`는 JavaScript에서 어떻게 작동하는지 설명해주세요.\*\*

**클로져(Closure)는 무엇이며, 어떻게/왜 사용하는지 설명해주세요**

**렉시컬 스코핑(lexical scoping)**

**스코프**는 함수를 호출할 때가 아니라 **선언**할 때 생깁니다. 호출이 아니라 선언요! 정적 스코프라

```jsx
var another = function () {
    var x = "local";
    function y() {
        alert(x);
    }
    return { y: y };
};
var newScope = another();

var newScope = (function () {
    var x = "local";
    return {
        y: function () {
            alert(x);
        },
    };
})();
```

`another();` 하는 순간 return에 의해 `{ y: function () { alert(x) } };`

가 newScope에 저장

**IIFE (즉시 호출 함수 표현식)**

`(function() {})();` 구문입니다. **IIFE(즉시 호출 함수 표현식)**이라고도 하고, **모듈 패턴**이라고도 하는데, 함수를 선언하자마자 바로 실행시켜버리는 것

**실행 컨텍스트**

컨텍스트의 네가지 원칙

-   먼저 전역 컨텍스트 하나 생성 후, 함수 호출 시마다 컨텍스트가 생깁니다.
-   컨텍스트 생성 시 컨텍스트 안에 **변수객체**(**arguments, variable), scope chain, this**가 생성됩니다.
-   컨텍스트 생성 후 함수가 실행되는데, 사용되는 변수들은 변수 객체 안에서 값을 찾고, 없다면 스코프 체인을 따라 올라가며 찾습니다.
-   함수 실행이 마무리되면 해당 컨텍스트는 사라집니다.(클로저 제외) 페이지가 종료되면 전역 컨텍스트가 사라집니다.

```jsx
var name = "zero"; // (1)변수 선언 (6)변수 대입
function wow(word) {
    // (2)변수 선언 (3)변수 대입
    console.log(word + " " + name); // (11)
}
function say() {
    // (4)변수 선언 (5)변수 대입
    var name = "nero"; // (8)
    console.log(name); // (9)
    wow("hello"); // (10)
}
say(); // (7)
```

1.

```jsx
'전역 컨텍스트': {
  변수객체: {
    arguments: null,
    variable: ['name', 'wow', 'say'],
  },
  scopeChain: ['전역 변수객체'],
  this: window,
}
```

2.

```jsx
'전역 컨텍스트': {
  변수객체: {
    arguments: null,
    variable: [{ name: 'zero' }, { wow: Function }, { say: Function }]
  },
  scopeChain: ['전역 변수객체'],
  this: window,
}
```

3.

```jsx
'say 컨텍스트': {
  변수객체: {
    arguments: null,
    variable: ['name'], // 초기화 후 [{ name: 'nero' }]가 됨
  },
  scopeChain: ['say 변수객체', '전역 변수객체'],
  this: window,
}
```

4.

```jsx
'wow 컨텍스트': {
  변수객체: {
    arguments: [{ word : 'hello' }],
    variable: null,
  },
  scopeChain: ['wow 변수객체', '전역 변수객체'],
  this: window,
}
```

**호이스팅이란**

-   호이스팅이란 변수를 선언하고 초기화했을 때 선언 부분이 최상단으로 끌어올려지는 현상

```jsx
console.log(zero); // 에러가 아니라 undefined
sayWow(); // 정상적으로 wow
function sayWow() {
    console.log("wow");
}
var zero = "zero";
```

→

```jsx
function sayWow() {
    console.log("wow");
}
var zero;
console.log(zero);
sayWow();
zero = "zero";
```

이런경우엔 에러 발생

```jsx
sayWow(); // (3)
sayYeah(); // (5) 여기서 대입되기 전에 호출해서 에러
var sayYeah = function () {
    // (1) 선언 (6) 대입
    console.log("yeah");
};
function sayWow() {
    // (2) 선언과 동시에 초기화(호이스팅)
    console.log("wow"); // (4)
}
```

**클로져란**

```jsx
var makeClosure = function () {
    var name = "zero";
    return function () {
        console.log(name);
    };
};
var closure = makeClosure(); // function () { console.log(name); }
closure(); // 'zero';
```

```jsx
"전역 컨텍스트": {
  변수객체: {
    arguments: null,
    variable: [{ makeClosure: Function }, 'closure'],
  },
  scopeChain: ['전역 변수객체'],
  this: window,
}
"makeClosure 컨텍스트": {
  변수객체: {
    arguments: null,
    variable: [{ name: 'zero' }],
  },
  scopeChain: ['makeClosure 변수객체', '전역 변수객체'],
  this: window,
}

"closure 컨텍스트":  {
  변수객체: {
    arguments: null,
    variable: null,
  scopeChain: ['closure 변수객체', 'makeClosure 변수객체', '전역 변수객체'],
  this: window,
}
```

### **JavaScript에서 this란?**

this는 어떻게 정의되었느냐가 아니라 **어떻게(how) 호출되었느냐** 에 따라 결정된다.

1. 단독으로 쓰인 this

```jsx
var x = this;
console.log(x); //Window
```

1. 함수 안에서 쓴 this

```jsx
var num = 0;
function addNum() {
    this.num = 100;
    num++;

    console.log(num); // 101
    console.log(window.num); // 101
    console.log(num === window.num); // true
}

addNum();
```

1. 메소드 안에서 쓴 this

```jsx
var person = {
    firstName: "John",
    lastName: "Doe",
    fullName: function () {
        return this.firstName + " " + this.lastName;
    },
};

person.fullName(); //"John Doe"
```

```jsx
var num = 0;

function showNum() {
    console.log(this.num);
}

showNum(); //0

var obj = {
    num: 200,
    func: showNum,
};

obj.func(); //200
```

메소드를 호출하면 해당 메소드를 호출한 객체로 this 가 바인딩 된다.

1. 이벤트 핸들러 안에서 쓴 this

```jsx
var btn = document.querySelector("#btn");
btn.addEventListener("click", function () {
    console.log(this); //#btn
});
```

이벤트 핸들러의 경우 이벤트를 받는 HTML요소가 this로 바인딩 된다.

1. 생성자 안에서 쓴 this

```jsx
function Person(name) {
    this.name = name;
}

var kim = new Person("kim");
var lee = new Person("lee");

console.log(kim.name); //kim
console.log(lee.name); //lee
```

생성자 함수가 생성하는 객체로 this가 바인딩 된다.

그러나 new 키워드를 빼면 this가 window에 바인딩 된다.

```jsx
var name = "window";
function Person(name) {
    this.name = name;
}

var kim = Person("kim");

console.log(window.name); //kim
```

참고 : [https://nykim.work/71](https://nykim.work/71)

1. 명시적 바인딩을 한 this (apply(), call(), bind())

```jsx

```

1. 화살표 함수로 쓴 this

```jsx
var Person = function (name, age) {
    this.name = name;
    this.age = age;
    this.say = function () {
        console.log(this); // Person {name: "Nana", age: 28}

        setTimeout(() => {
            console.log(this); // Person {name: "Nana", age: 28}
            console.log(this.name + " is " + this.age + " years old");
        }, 100);
    };
};
var me = new Person("Nana", 28); //Nana is 28 years old
```

### Call by reference vs Call by value

원시 데이터 타입 - number, string, boolean, undefined, null

객체 - Array, object, function

이때 원시 데이터 타입은 **값** 으로 전달되고 객체는 **참조** 로 \*\*\*\*전달된다.

```jsx
let name = "jacob";
function changeName(name) {
    name = "master jung";
    return name;
}

console.log(changeName(name)); // master jung
console.log(name); // jacob
```

**참조하고 있는 메모리 주소**가 아닌 **값**으로 전달되기 때문에 함수에서 변수에 대한 모든 변경 사항이 함수 외부에서 발생하는 변수와 완전히 분리되고, 값을 변경해도 원래 값의 실제 참조는 업데이트 되지 않는다.

```jsx
let nameObj = {
    name: "jacob",
};
function changeName(nameObj) {
    return (nameObj.name = "master jung");
}

console.log(changeName(nameObj)); // master jung
console.log(nameObj); // master jung
```

왜냐하면 객체로 전달하면 값이 아닌 **참조**로 전달되기 때문에

```jsx
let nameObj = {
    name: "jacob",
};
function changeName(nameObj) {
    nameObj = {
        name: "master jung",
    };
    return nameObj;
}

console.log(changeName(nameObj)); // master jung
console.log(nameObj); // jacob
```

이유는 Call by sharing 때문

함수가 참조를 새 객체 또는 배열에 대한 참조로 덤어 쓰면 새로운 메모리에 참조되며, 외부 객체에 영향을 주지 않는다.

### JSON 과 AJAX

json이란 Javascript object notation

클라이언트와 서버 간 데이터 교환을 위한 규칙 즉 데이터 포맷

Ajax(Asynchronous JavaScript and XML)는 자바스크립트를 이용해서 **비동기적(Asynchronous)**으로 서버와 브라우저가 데이터를 교환할 수 있는 통신 방식

### ==과 ===

== 은 동등(coercive) 연산자

=== 은 일치(strict) 연산자

-   '==' 연산자를 이용하여 서로 다른 유형의 두 변수의 [값] 비교
-   '==='는 엄격한 비교를 하는 것으로 알려져 있다 ([값 & 자료형] -> true).

### undefined vs null vs undeclared

null

-   변수를 선언하고 빈 변수임을 정해준다

```jsx
let n = null;
console.log(n); // null
console.log(typeof n); // object
```

undefined

-   변수를 선언하고 값을 할당하기 전의 값이며 변수에 할당되어 있지 않은 상태

```jsx
let b;
console.log(b); // undefined
console.log(typeof b); // undefined
```

undeclared(미선언 변수)

-   접근 가능한 스코프에 변수 선언조차 되어있지 않은 상태

```jsx
console.log(f); // Uncaught ReferenceError: f is not defined at <anonymous>:1:13
```

### let vs var vs const

우선, `var`는 변수 선언 방식에 있어서 큰 단점을 가지고 있다.

```
    var name = 'bathingape'
    console.log(name) // bathingape

    var name = 'javascript'
    console.log(name) // javascript
```

변수를 한 번 더 선언했음에도 불구하고, 에러가 나오지 않고 각기 다른 값이 출력되는 것을 볼 수 있다.

그렇다면 `let` 과 `const` 의 차이점은 무엇일까?

이 둘의 차이점은 `immutable` 여부이다.

`let` 은 변수에 재할당이 가능하다. 그렇지만,

```jsx
let name = "bathingape";
console.log(name); // bathingape

let name = "javascript";
console.log(name);
// Uncaught SyntaxError: Identifier 'name' has already been declared

name = "react";
console.log(name); //react
```

`const`는 변수 재선언, 변수 재할당 모두 불가능하다.

```jsx
const name = "bathingape";
console.log(name); // bathingape

const name = "javascript";
console.log(name);
// Uncaught SyntaxError: Identifier 'name' has already been declared

name = "react";
console.log(name);
//Uncaught TypeError: Assignment to constant variable.
```

let, const 는 블록 레벨 스코프

let, const 키워드로 선언한 변수는 모두 코드 블록(ex. 함수, if, for, while, try/catch 문 등)을 지역 스코프로 인정하는 블록 레벨 스코프를 따른다.

### 자바스크립트 동작 원리

Callback Event Queue에서 하나 씩 꺼내 동작시키는 Loop.

자바스크립트는 단일 스레드 기반 언어이기 때문에 한번에 하나씩 작업을 진행한다. 그러나 자바스크립트가 사용되는 환경을 생각해보면 많은 작업이 동시에 처리되고 있는 걸 볼 수 있다.

자바스크립트는 이벤트 루프를 이용해서 비동기 방식으로 동시성을 지원한다.

**call stack**

Call stack은 함수의 호출을 저장하는 자료구조이다. 어떤 함수를 호출하면 스택에 쌓고 또 다른 함수를 호출하면 그 다음 스택에 쌓으면서 가장 위에 쌓인 함수를 가장 먼저 처리

**메모리 힙**

-   구조화되지 않은 넓은 메모리 영역을 말한다.
-   객체들이 할당된다
    -   프로그램에 선언한 변수, 함수 등

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bf55f2c5-239f-40c8-887c-14e954ef1102/Untitled.png)

### promise란

프로미스는 자바스크립트 비동기 처리에 사용되는 객체

-   Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태
-   Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
-   Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태

ES6 문법

-   const and let
-   Arrow functions(화살표 함수)
-   Template Literals(템플릿 리터럴)
-   Default parameters(기본 매개 변수)
-   Array and object destructing(배열 및 객체 비구조화)
-   Import and export(가져오기 및 내보내기)
-   Promises(프로미스)
-   Rest parameter and Spread operator(나머지 매개 변수 및 확산 연산자)
-   Classes(클래스)

## 3. 즉시 실행 함수를 사용하는 이유

### 초기화

즉시 실행 함수는 한 번의 실행만 필요로 하는 초기화 코드 부분에 많이 사용된다.그 이유는 **변수를 전역으로 선언하는 것을 피하기 위해서** 이다. 전역에 변수를 추가하지 않아도 되기 때문에 코드 충돌 없이 구현할 수 있어서 플러그인이나 라이브러리 등을 만들 때 많이 사용된다.
