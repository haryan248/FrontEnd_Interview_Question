event delegation에 관해 설명해주세요.

**Event Bubbling(이벤트 버블링)**

-   이벤트 버블링은 특정 화면 요소에서 이벤트가 발생했을 때 해당 이벤트가 더 상위의 화면 요소들로 전달되어 가는 특성

![image](https://user-images.githubusercontent.com/51049245/142718365-eb6d5254-2683-4422-8981-f46227faed56.png)

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

![image](https://user-images.githubusercontent.com/51049245/142718379-14589e49-76bd-41fc-a661-0c90d71067c3.png)

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

**클로져를 사용하는 이유?**

1. 상태 유지: 현재 상태를 기억하고 변경된 최신 상태를 유지할 수 있다.
2. 전역 변수의 사용 억제: 상태 변경이나 가변 데이터를 피하고 오류를 피하는 안정성을 증가 시킬수 있다.
3. 정보의 은닉: 클래스 기반 언어의 private 키워드를 흉내낼 수 있다.

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

![image](https://user-images.githubusercontent.com/51049245/142718387-2d1d9141-c760-4f83-8b4f-2c13034def99.png)

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

## 최소한의 메모리 관리에 신경 쓰는 방법

### **1. 의도치 않은 전역 변수 생성을 막기**

**자바스크립트는 선언되지 않고 사용한 변수를 전역 변수로 처리하도록 되어 있다.**

```jsx
function(){
  foo = "inyong~";
}

// 실행 시 아래와 동일function(){
  window.foo = "inyong~";// window는 브라우저 내 최상단 DOM 오브젝트
}
```

var, let, const를 선언하지 않고 사용하게 되면, 해당 변수는 전역 객체의 하위 오브젝트로 지정됨으로써 전역 변수로 사용된다. 이로 인해 foo변수는 사용하지 않더라도 계속해서 불필요한 메모리로 남게 될 것이다.

또한 this를 이용해서도 뜻하지 않은 전역 변수를 생성할 수도 있다. 아래 예시를 봐보자.

```jsx
function foo() {
    const bar = {
        a: function () {
            console.log(this);
        },
    };
    // bar.a(); // {a:f함수} 출력
}

foo();
```

this는 자신을 감싸고 있는 오브젝트를 가리킨다. 그래서 위 코드에서는 this 감싸고 있는 오브젝트는 bar인 것을 알 수 있다. 그러나 아래 코드를 확인해보자.

```jsx
function foo() {
    this.bar = "potential accidental global";
}
// 다른 함수 내에 있지 않은 foo를 호출하면 this는 글로벌 객체(window)를 가리킴
foo();
```

여기서는 this를 감싸고 있는 특정 오브젝트가 없다. 정확히 말하면 글로벌 오브젝트인 window가 감싸고 있는 형태이므로 여기서 this는 window를 가리키게 된다. 그래서 위처럼 this.bar를 이용하게 되면 해당 bar 변수도 전역 변수가 되어버리고 만다.

이러한 방식은 의도적으로 가비지 컬렉터가 정리할 수 없게 하기 위해 전역 변수 방식으로 사용할 수도 있지만, 그것이 아니고 임시로 정보를 저장하여 사용하는 것, 특히나 많은 양의 정보를 처리할 때 사용하는 용도라면 이러한 점을 조심해야 할 것이다.

### **2. 잊혀진 타이머 혹은 콜백 함수**

자바스크립트에 많이 사용되는 타이머 함수와 콜백 함수로 인해서도 메모리 누수가 발생할 수 있다.아래의 setInterval을 예시로 확인해보자.

```jsx
function timeRun() {
    var serverData = "hello~inyong";

    setInterval(function () {
        var element = document.getElementById("someID");
        if (element) {
            element.innerHTML = JSON.stringify(serverData);
        }
    }, 5000); // 매 5초 마다 실행
}

timeRun();
```

위 코드에서 보면 매 5초마다 특정 DOM 엘리먼트를 가져와서 하위로 serverData 변수 값을 주입한다. 해당 이벤트는 계속 활성화 상태가 되므로 해당 이벤트에 연결되어 있는 serverData 변수 메모리도 계속해서 사용하는 것으로 간주되어 그대로 남아있다.

그러나 해당 엘리먼트는 다른 곳에서 언제든지 제거할 수 있는 가능성을 가지고 있고, 만약 제거가 된다면 serInterval()의 타이머 함수는 더 이상 의미 없는 이벤트 동작이 된다.

그럼에도 불구하고 해당 setInterval 이벤트는 아직 활성 상태이므로 가비지 컬렉터가 이 이벤트 핸들러와 해당 이벤트 내부에서 사용되는 메모리들을 해제하지 않게 되고 5초마다 의미 없는 이벤트가 계속해서 동작하여 CPU의 낭비를 초래하게 된다.

그나마 다행인 것은 serverData 변수에 할당된 메모리는 더 이상 사용하고 있는 곳이 없고 접근할 수 있는 연결고리가 없으므로 바로 가비지 컬렉션이 일어난다. 만약 serverData 변수가 setInterval 이벤트 내부에 있었으면 이 변수 또한 그대로 불필요한 메모리를 차지하고 있었을 것이다.

그렇기에 이러한 타이머 함수를 사용할 때는 해당 타이머의 이벤트가 더 이상 의미가 없어졌을 때, 꼭 명시적으로 그것을 제거해야 할 필요가 있다.

### **3. 클로저**

우선 여기 부분을 이해하려면 스코프 체이닝에 대한 개념을 잘 알고 있어야 한다. 클로저를 이용하게 되면 함수가 끝나도 아직 스코프 체인이 그대로 남아 있어서 끝났던 함수 내의 요소들을 참조할 수 있으므로 메모리에서 사라지지 않는다.

Meteor라는 개발자들이 해당 클로저로 인해 발생하는 메모리 누수의 [특정 사례](https://blog.meteor.com/an-interesting-kind-of-javascript-memory-leak-8b47d2e7f156)에 대해 설명한 글을 봤는데, 정말 너무 이해가 안 갔었다.. 이해하는데 이틀 정도 걸렸던 것 같다...

우선 같이 코드를 봐보자.

```jsx
var theThing = null;

var replaceThing = function () {
    var originalThing = theThing;

    theThing = {
        longStr: new Array(1000000).join("*"),
        someMethod: function () {
            console.log(someMessage);
        },
    };
};

setInterval(replaceThing, 1000);
```

위 코드를 보면 replaceThing 함수를 1초에 한 번씩 실행시키는데, 아래에서 동작 과정을 나열해보겠다. 편의 상, 첫 번째로 호출된 replaceThing을 replaceThing(1), 두 번째 호출은 replaceThing(2)로 작성하겠다.

1. replaceThing(1)은 theThing 전역 변수에 새 오브젝트는 넣는다. originalThing은 null이다.
2. 그다음 replaceThing(2)이 호출되고, originalThing에는 전역 변수 theThing에 의해 replaceThing(1)에서 생성되었던 값을 참조하게 한다.
3. 그다음 전역 변수 theThing에 다시 새로운 값을 넣는다. 이때 생성된 값 중 내부 함수인 someMethod는 originalThing을 참조할 수 있다. (위 코드에서는 실제로는 참조는 안 하고 있지만, 더 내부에 있는 someMethod는 바로 부모 스코프인 영역들을 참조할 수 있도록 스코프 체인을 이루고 있으면 메로리 해제를 하지 않는다.)
4. 현재 replaceThing(2)의 originalThing 변수는 이전 replaceThing(1)을 참조하고 있다. 그리고 현재 replaceThing(2)에서 새로 만든 theThing의 값은 originalThing을, 즉 이전에 만들었던 값과 스코프 체인을 이루게 되는 것이다.

그래서 결국 replaceThing이 호출될 때마다 이전의 theThing과 새로운 theThing이 계속해서 스코프 체인이 이루어지므로 참조할 수 있는 영역으로 판단하여 가비지 컬렉션이 이루어지지 않아야 한다.

하지만 구글의 V8 엔진에서는 멋지게도 이러한 요소들까지 고려하여 setInterval 함수로 인해 불필요하게 스코프 체이닝이 일어나면 이전의 스포크 체인을 없애준다. 그래서 위 코드는 setInterval이 동작할 때마다 메모리가 일정하게 된다.

하지만 문제의 코드는 바로 아래이다.

```jsx
var theThing = null;

var replaceThing = function () {
  var originalThing = theThing;

  var unused = function () {
    if (originalThing)// 'originalThing'에 대한 참조console.log("hi");
  };

  theThing = {
    longStr: new Array(1000000).join('*'),
    someMethod: function () {
      console.log("message");
    }
  };
};
setInterval(replaceThing, 1000);
```

위 코드의 동작 과정을 확인해보자.

1. replaceThing(1)은 theThing 전역 변수에 새 오브젝트는 넣는다. originalThing은 null이다.
2. 그다음 replaceThing(2)이 호출되고, originalThing에는 전역 변수 theThing에 의해 replaceThing(1)에서 생성되었던 값을 참조하게 한다.
3. 그다음 내부 함수인 unused 변수를 생성한다. unused는 originalThing을 사용한다. 즉, 현재 replaceThing(2)의 ununsed 내부 함수 안에 replaceThing(1)의 someMethod 내부 함수가 있는 것이다. 정리하면 replaceThing함수 내부에 unused 내부 함수에 someMethod 내부 함수가 있는 것임. 3중 내부 함수.
4. 그다음 전역 변수 theThing에 다시 새로운 값을 넣는다. 이때 생성된 값 중 내부 함수인 someMethod는 originalThing과 unused를 참조할 수 있다.(여기서 중요!) 이때 someMethod가 참조하고 있는 unused는 내부 함수이다. 여기까지만 생각하면 unused 변수 위에 originalThing(이전에 생성된 값)의 someMethod와 스코프를 이루는 것과 같이 차이가 없다. (원래는 스코프 체이닝 연결이 돼서 가비지 컬렉션이 이루어지지 않아야 되는 것을 위에 말했듯이 멋쟁이 구글 V8가 이를 알아서 처리해줌)하지만 unused의 내부 함수는 또 하나의 내부 함수를 포함하고 있다. (originalThing, 즉 이전에 생성된 someMethod 함수)그러니까 결국 replace(2)에서 생성된 someMethod 함수는 바로 상위의 unused 함수와 스코프 체인을 이루면서도 unused 함수의 내부 함수 someMethod(replace(1)에서 생성했던 값)까지 스코프 체인을 이루게 되는 것이다.

이렇게 더 깊이 스코프 체이닝이 이루어지는 것은 V8에서 처리를 하지 못하는 것 같다. 그래서 결국 replaceThing이 실행이 될 때마다 계속해서 스코프 체이닝이 이루어지고 참조할 수 있는 것으로 판단하여 메모리가 계속해서 증가하게 된다.

### **4. DOM에서 벗어난 요소 참조**

DOM 엘리먼트들을 빠르게 불러와서 바로 사용하기 위해 특정 데이터 요소에 저장하여 사용하는 경우가 있다. 예를 들면 아래 코드에서 첫 번째 줄처럼 사용할 수도 있고, 혹은 특정 배열에 저장해서 사용할 수도 있을 것이다. 그러나 만약 이렇게 사용 중인 엘리먼트를 제거하기로 결정하면, DOM 트리 자체에서 제거하는 것뿐 아니라, 변수에 저장하여 참조하고 있는 연결고리도 함께 제거해 주어야 한다는 것을 잊으면 안 된다.

```jsx
var elements = {
    button: document.getElementById("button"),
    image: document.getElementById("image"),
};

function doStuff() {
    elements.image.src = "http://example.com/image_name.png";
}

function removeImage() {
    // image는 body 요소의 바로 아래 자식임document.body.removeChild(document.getElementById('image'));
    // 이 순간까지 #button 전역 요소 객체에 대한 참조가 아직 존재함// 즉, button 요소는 아직도 메모리 상에 있고 가비지컬렉터가 가져갈 수 없음
}
```

위 코드에서 removeImage() 함수를 실행시키면, image DOM 오브젝트가 DOM Tree에서는 삭제가 되므로 화면 상에서는 사라질 것이다. 그러나 해당 DOM 오브젝트는 첫 번째 줄의 elements변수에서 아직 참조를 하고 있는 중이므로 가비지 컬렉션이 일어나지 않게 되고 메모리 누수가 일어나게 된다.

같은 경우에 대해 더욱 극심한 예시도 있다. 아래 코드를 확인해보자.

```jsx
var elements = {
    td: document.getElementById("td"), // <table> 내 셀 태그인 <td>
};

function removeTable() {
    document.body.removeChild(document.getElementById("tableID")); // <table> 태그 제거// td 엘리먼트가 아직 참조 중이므로, 모든 table 내 데이터가 그대로 유지
}
```

DOM Tree에서 Table DOM 엘리먼트를 제거했다. 그러나 Table 오브젝트의 하위인 td 셀 태그 엘리먼트가 여전히 참조되고 있다. td 엘리먼트는 table엘리먼트를 참조하고 있으므로 해당 td 뿐 아니라 Table DOM 엘리먼트 내에서 사용되던 많은 오브젝트들이 메모리에서 제거되지 않고 여전히 남아있게 되어 커다란 누수가 일어나게 되는 것이다.

```jsx
function useTd() {
    var elements = {
        td: document.getElementById("td"), // <table> 내 셀 태그인 <td>
    };
}

function removeTable() {
    document.body.removeChild(document.getElementById("tableID")); // <table> 태그 제거
}

useTd();
removeTable();
```

다행히도 위 코드와 같이 td참조 방식이 전역 변수 관리가 아닌 함수 내 지역 변수로 잠깐 이용하는 것이라면, Table 오브젝트가 DOM Tree가 삭제되면서 정상적으로 가비지 컬렉션이 일어날 것이다. 왜냐하면  DOM Tree로 Table 오브젝트가 삭제된 뒤 useTd() 함수 내에서 elements 변수가 참조를 하고 있지만, 최상위 roots 오브젝트에서 더 이상 elements 변수에 접근할 수 없게 되었으므로 '표시하고-쓸기(Mark-and-weep)'에 의해 가비지 컬렉션 대상이 되어버리기 때문이다.

## Virtual DOM의 사용목적

-   DOM 을 자주 변경하여 퍼포먼스를 하락시키는 것을 피하기 위함
-   가볍고 효과적으로 Virtual DOM과 DOM 사이의 차이를 계산하기 위해 사용하는 것입니다.

1. 초기 Virtual DOM의 상태는 실제 DOM에 존재하던 요소들과 동일합니다.
2. 특정한 변화가 발생한 경우, 그 두 상태의 차이를 비교합니다.
3. 변경된 결과만 실제 DOM에 적용됩니다.
4. Virtual DOM이 실제 DOM과 비교하면서 업데이트 되었기 때문에, 전체 Object를 복사하지 않으면서, Virtual DOM은 실제 DOM의 가장 최신 상태를 보유하게 됩니다.
