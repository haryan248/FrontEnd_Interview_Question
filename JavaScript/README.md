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
