### 구글을 입력하면 벌어지는 일

1. www.google.com을 브라우저 주소창에 친다

2. Browser는 캐싱된 DNS 기록들을 통해 www.google.com에 대응되는 IP 주소가 있는지 확인한다

3. 요청한 URL이 캐시에 없으면, ISP의 DNS 서버가 www.google.com을 호스팅하고 있는 서버의 IP 주소를 찾기 위해 DNS query를 날린다.

4. Browser가 서버와 TCP connection을 한다(TCP 3way- handshaking)

5. Browser가 웹 서버에 HTTP 요청을 한다.

6. 서버가 요청을 처리하고 response를 생성한다

7. 서버가 HTTP response를 보낸다

8. Browser가 HTML content를 보여준다

[https://devjin-blog.com/what-happen-browser-search/](https://devjin-blog.com/what-happen-browser-search/)

### 브라우저의 동작 원리(랜더링 원리)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b2fcfcc4-2f10-40d6-95f6-6fc646fad706/Untitled.png)

-   사용자 인터페이스: 주소 표시줄, 이전/다음 버튼, 북마크 등 페이지 뷰 이외의 다른 부분
-   브라우저 엔진: 사용자 인터페이스와 렌더링 엔진 사이 동작 제어
-   렌더링 엔진: HTML, CSS를 파싱해 화면에 요청한 컨텐츠를 표시
-   통신: HTTP요청과 같은 네트워크 호출에 사용됨
-   JS 엔진: 자바스크립트 코드를 해석하고 실행
-   UI 백엔드: 기본적인 위젯(콤보 박스 등)을 그림
-   자료 저장소: 자료를 저장하는 계층으로 쿠키 등을 저장하는 웹 데이터베이스

1. HTML 마크업을 처리하고 DOM 트리를 빌드한다. (**"무엇을"** 그릴지 결정한다.)
2. CSS 마크업을 처리하고 CSSOM 트리를 빌드한다. (**"어떻게"** 그릴지 결정한다.)
3. DOM 및 CSSOM 을 결합하여 렌더링 트리를 형성한다. (**"화면에 그려질 것만"** 결정)
4. 렌더링 트리에서 레이아웃을 실행하여 각 노드의 기하학적 형태를 계산한다. (**"Box-Model"** 을 생성한다.)
5. 개별 노드를 화면에 페인트한다.(or 래스터화)

### CORS란?(Cross-Origin Resource Sharing) 와 SOP

다른 도메인으로부터 리소스가 요청될 경우 해당 리소스는 **cross-origin HTTP 요청** 에 의해 요청된다. 하지만 대부분의 브라우저들은 보안 상의 이유로 스크립트에서의 cross-origin HTTP 요청을 제한한다. 이것을 `Same-Origin-Policy(동일 근원 정책)`이라고 한다. 요청을 보내기 위해서는 요청을 보내고자 하는 대상과 프로토콜도 같아야 하고, 포트도 같아야 함을 의미한다.

포트까지 모두 일치해야 같은 origin이라고 판단하고 같은 출처의 경우에만 허용

**장점**

동일 출처 정책을 지키면 외부 리소스를 가져오지 못해 불편하지만, 동일 출처 정책은 [XSS](https://ko.wikipedia.org/wiki/%EC%82%AC%EC%9D%B4%ED%8A%B8_%EA%B0%84_%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8C%85)나 [XSRF](https://ko.wikipedia.org/wiki/%EC%82%AC%EC%9D%B4%ED%8A%B8_%EA%B0%84_%EC%9A%94%EC%B2%AD_%EC%9C%84%EC%A1%B0) 등의 보안 취약점을 노린 공격을 방어

**CORS 동작 방식**

라우저는 요청 헤더에 **`Origin`**이라는 필드에 요청을 보내는 출처를 함께 담아보낸다.

**`Access-Control-Allow-Origin`**이라는 값에 “이 리소스를 접근하는 것이 허용된 출처”를 내려주고, 이후 응답을 받은 브라우저는 자신이 보냈던 요청의 **`Origin`**과 서버가 보내준 응답의 **`Access-Control-Allow-Origin`**을 비교해본 후 이 응답이 유효한 응답인지 아닌지를 결정

**Preflight Request(예비 요청)**

서버에 예비 요청을 보내서 안전한지 판단한 후 본 요청을 보내는 방법

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bfb2d0f4-7560-49eb-976b-2a2238c6ffa1/Untitled.png)

**Simple Request**

-   예비요청을 보내지 않고 바로 서버에게 본요청을 보낸후 CORS 정책 위반여부를 검사
-   이는 특정 조건을 만족하는 경우에만 예비 요청을 생략할 수 있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7f896f57-00c8-4ec9-ad45-57ba4dd01ed0/Untitled.png)

-   요청 메서드(method)는 GET, HEAD, POST 중 하나여야 합니다.
-   Accept, Accept-Language, Content-Language, Content-Type, DPR, Downlink, Save-Data, Viewport-Width, Width를 제외한 헤더를 사용하면 안 됩니다.
-   Content-Type 헤더는 application/x-www-form-urlencoded, multipart/form-data, text/plain 중 하나를 사용해야 합니다.

CORS 에러 해결 방법

-   `Access-Control-Allow-Origin` 헤더에 작성된 출처만 브라우저가 리소스를 접근할 수 있도록 허용합니다
-   프록시 서버 : 프론트엔드와 백엔드 사이에 프록시 서버를 두는 방법으로 CORS를 해결

### 바벨과 폴리필

폴리필은 **런-타임**에 필요한 기능을 주입

브라우저에서 실행되는 시점에 필요한 기능을 주입

바벨은 **구 브라우저**에서도 최신자바스크립트 코드를 작동하도록 변환해주는 컴파일러(혹은 트랜스파일러)

**_Promise, Map, Set 같은 전역객체_**들이나 **_String.padStart등 전역 객체에 추가된 메서드_**등 컴파일-타임의 코드변환으로는 해결하기 어렵기 때문에 **_폴리필(polyfill)_** 이 필요한 것

### 웹팩(webpack)이란?

웹팩이란 최신 프런트엔드 프레임워크에서 가장 많이 사용되는 **[모듈 번들러(Module Bundler)](https://joshua1988.github.io/webpack-guide/webpack/what-is-webpack.html)**입니다. 모듈 번들러란 웹 애플리케이션을 구성하는 자원(HTML, CSS, Javscript, Images 등)을 모두 각각의 모듈로 보고 이를 조합해서 병합된 하나의 결과물을 만드는 도

**웹팩으로 해결하려는 문제?**

-   자바스크립트 변수 유효 범위
-   브라우저별 HTTP 요청 숫자의 제약
-   사용하지 않는 코드의 관리
-   Dynamic Loading & Lazy Loading 미지원

## import vs require 차이

모듈 시스템은 CommonJS 방식에 비해 코드의 직관성이 좋고, 비동기 방식으로 작동하면서 불러오는 모듈의 실제로 사용되는 부분들만 로드하기 때문에 성능적으로도 효율적
