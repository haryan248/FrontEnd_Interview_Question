## HTML

**DOCTYPE 이란 무엇인가요?**

-   "문서 형식 선언"(Document Type Declaration), 또는 doctype이란 문서의 유형을 정의하기 위해 사용하는 선언문
-   웹 문서의 시작을 알려주며 태그보다 먼저 선언한다. DOCTYPE은 웹 브라우저에서 처리할 문서가 HTML이며 어떠한 버전으로 사용했으니, 해당 방식대로 해석하라는 의미를 갖는다
-   브라우저들이 저마다의 기준대로 랜더링을 실시
    -   올바른 DOCTYPE을 인식하지 못하면 quirks mode를 트리거한다.

**여러 meta 태그들에 대한 질문**

**시맨틱 태그란 무엇인가요?**

-   시맨틱(Semantic)은 "의미의, 의미론적인" 이라는 뜻, 즉 시맨틱 태그란 의미를 가지는 태그이다.
    -   개발자가 의도한 요소의 의미가 명확히 드러나고 있다.이것은 코드의 가독성을 높이고 유지보수를 쉽게한다.
        > **non-semantic 요소**
        > form, table, img 등이 있으며 이들 태그는 content의 의미를 명확히 설명한다.
        > **semantic 요소**
        > form, table, img 등이 있으며 이들 태그는 content의 의미를 명확히 설명한다.

**이미지 태그에 `srcset` 속성을 사용하는 이유는 무엇인가요? 브라우저가 이 속성을 가진 콘텐츠를 평가할 때 사용하는 과정을 설명해보세요.**

-   srcset 속성은 각각 다른 환경에서 사용될 이미지 소스를 명시
-   srcset 속성은 브라우저가 사용할 수 있는 이미지 소스를 나타내는 하나 이상의 문자열을 콤마(,)로 결합한 리스트를 속성값으로 가집니다.

### **여러 언어로 되어 있는 콘텐츠의 페이지를 어떻게 제공하나요?**

-   여러 언어로 제공되는 페이지를 제공하기 위해선 페이지 내의 내용이 하나의 일관된 언어로 표시되어야 한다. 브라우저가 HTTP 요청을 서버에 보내면, 대게 Accept-Language와 같은 기본 언어에 대한 설정 정보를 보낸다. 서버는 이 정보를 확인하고 해당 언어에 맞는 문서를 반환한다. 이 때 태그의 lang 속성을 선언해줘야 한다.
-   서버는 일반적으로 백엔드 프레임워크의 도움을 받아, 특정 언어로 HTML 마크업에서 YML 또는 JSON 형식의 특정 언어에 대한 placeholder와 내용을 포함하여 HTML 페이지를 동적 생성한다.

### **다국어 사이트를 디자인하거나 개발할 때 주의해야할 사항은 무엇인가요?**

-   HTML lang 속성을 빠뜨려선 안됩니다.
-   사용자가 번거롭지 않도록 쉽게 국가/언어를 변경할 수 있도록 합니다.
-   이미지에 텍스트가 없어야 합니다. 여러 개의 이미지를 준비해야 하기 때문에 작업이 번거로워 집니다.
-   일부 언어는 다른 언어로 작성될 때 더 길어질 수도 있으므로, 디자인에 레이아웃이나 오버 플로우 문제 발생에 주의해야 합니다. 제목, 레이블, 버튼과 같은 항목에서 문자 수 제한을 두는 것이 좋습니다.
-   국가별 날짜와 통화 형식에 유의합니다.
-   번역된 문자열을 연결하는 대신, 각 언어에 대한 매개변수와 함께 템플릿 스트링을 사용합니다.
-   언어를 읽는 방향에 유의합니다.

### **data- 속성은 무엇에 좋은가요?**

-   JavaScript 프레임워크가 인기 있기 전, DOM 자체에서 상태 값을 저장하기 위해 data- 속성을 사용했다. 이는 적절한 속성이나 요소가 없는 페이지나 애플리케이션에 사용자 정의 데이터를 비공개로 저장하기 위해 사용했다.
-   그러나 개발자 도구를 통해 손쉽게 데이터를 변경할 수 있으므로 사용을 권장하지 않는다.
-   따라서 리덕스와 같은 상태관리 라이브러리나 프레임워크의 데이터 바인딩을 통해 DOM을 업데이트된 상태로 유지하는 편이 낫다.

### **HTML5를 개방형 웹 플랫폼으로 간주할 때, HTML5의 구성요소는 무엇인가?**

-   main, footer, nav 등 의미론적 태크(semantic tag)가 추가돼, 콘텐츠의 구조를 더 명확히 설명할 수 있다.
-   더 새롭고 혁신적인 방법으로 서버와 통신할 수 있게 되었다.
-   브라우저의 로컬 스토리지를 활용하여, 웹 페이지가 브라우저에 데이터를 로컬로 저장할 수 있게 되었다. 이를 통해, 오프라인에서도 효율적으로 작동할 수 있게 되었다.
-   플러그인의 도움 없이 비디오나 오디오를 웹에서 조작할 수 있게 되었다.
-   컴퓨터 하드웨어의 성능 최적화와 개선으로 더 나은 사용을 제공한다
-   다양한 입출력 장치의 사용을 허용한다.
-   사용자가 더 세련된 테마를 사용할 수 있다.
-   2D/3D 그래픽과 효과를 사용할 수 있어, 훨씬 다양한 프레젠테이션 옵션을 허용합니다.

### **cookie, sessionStorage, localStorage 사이의 차이점을 설명하세요.**

-   공통점 : 모두 브라우저에 객체(Key-value) 형식으로 값을 저장할 수 있는 저장소이다. 다만, 형식은 String으로 제한된다.
-   차이점
    -   생성 방법 : 쿠키는 서버 측에서 Set-Cookie 헤더를 사용하거나 브라우저에서 직접 생성할 수 있다. local과 session은 클라이언트(브라우저)에서 생성한다.
    -   만료 : 쿠키는 수동으로 설정하나, local은 영구적이며 Session은 브라우저 탭을 닫을 때 만료된다.
    -   브라우저 세션 전체에서 지속 : Local에서만 가능하며, 쿠키는 만료 설정 여부에 따라 다르다.
    -   HTTP 요청과 함께 서버로의 전송 여부 : 쿠키만 전송되며, 이는 Cookie 헤더를 통해 자동 전송된다.
    -   용량 : 쿠키 (4kb), local/session (5MB)
    -   접근성 : session만 같은 탭에서 지속되며, 쿠키와 local은 모든 윈도우에서 접근 가능하다.

### **script, script async, script defer 사이의 차이점은 무엇인가?**

-   문서 파일에 자바스크립트를 추가하는 방식은 위 방법처럼, 총 3가지이다. 각각 스크립트 파일이 파싱되는 방식이 서로 다르다. 먼저 script 태그를 추가하면, HTML이 중단되고 스크립트 파싱을 시작하고 끝난 후에야 HTML 파싱이 진행된다. script async 태그는 HTML 파싱과 스크립트 파싱이 동시에 이뤄지고 완료된 순서대로 시행된다. script defer 태그는 HTML과 스크립트가 동시에 파싱되고 스크립트의 실행은 HTML의 파싱이 다 이뤄진 후에 완료된다.
-   주의할 점은 src 속성이 없는 스크립트 태그는 async와 defer 적용이 무시된다는 점이다. 그러니 꼭 추가하자.

### **왜 일반적으로 CSS link 태그를 head, /head 태그 사이에 위치시키고, JS script 태그를 /body 직전에 위치시키는 것이 좋은 방법인가요? 다른 예외적인 상황을 알고있나요?**

-   link를 head 안에 넣어야 최적화된 웹사이트를 구축할 수 있다. 문서 상단에 위치한 head 태그 안에 CSS 파일을 위치시켜야, HTML 파일과 동시에 CSS 파일이 점진적으로 렌더링될 수 있기 때문이며, 이는 사이트 성능 점수의 사이트 최적화에 포함된다.
-   또 /body 직전에 script 태그를 넣는 까닭은 script가 파싱되는 동안, HTML 파싱이 이뤄지지 않기 때문이다. 근데 HTML 문서의 끝지점인 /body 직전에 script 태그를 두면 HTML이 파싱된 후, 스크립트 태그를 파싱할 수 있다. (단, 앞서 보았듯 defer 속성을 두면 head 태그에 둬도 상관 없다)

### **프로그레시브 렌더링이 무엇인가요?**

-   프로그레시브 렌더링이란 콘텐츠를 가능한한 빠르게 표시하기 위해 웹 페이지의 성능을 향상시키는 데 사용되는 기술이다. 예를 들어, 페이지의 이미지를 한꺼번에 로딩하지 않고 로딩하는 컨텐츠의 우선순위를 설정하는 방식을 말한다. 주로 가능한 한 빨리 화면에 표시해야 하는 콘텐츠의 우선순위를 높게 설정한다.

### **이미지 태그에 srcset 속성을 사용하는 이유는 무엇인가요?**

-   `srcset` 속성은 사용자의 디스플레이 사양에 따라 다른 해상도의 이미지를 제공함으로써 사용자 경험을 높이기 위해 사용한다. 구체적으로 고사양 디스플레이에는 고품질 이미지를 제공하고 저사양 기기에는 저해상도 이미지를 제공한다.
-   방법은 다음과 같다. img srcset="small.jpg 500w, medium.jpg 1000w, large.jpg 2000w" src="..." alt=""는 클라이언트의 해상도를 계산해, 알맞은 그래픽 이미지를 제공한다. 이미지의 너비가 320px일 때, small.jpg는 500 / 320 = 1.5626, medium.jpg는 1000 / 320 = 3.125, large.jpg는 2000 / 320 = 6.25로 계산한다. 해상도가 1.xx일 경우 small.jpg을 선택하고 해상도가 2.xx인 경우 그 이상의 값을 제공하는 medium.jpg를 사용한다. 이처럼 `srcset` 속성을 통해 클라이언트의 해상도에 따라 브라우저에 small, medium, large .jpg 그래픽을 표시하도록 지시할 수 있다.
