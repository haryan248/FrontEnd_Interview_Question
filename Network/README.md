# 1. HTTP (GET vs POST)

### GET 방식

우선 GET 방식은 요청하는 데이터가 `HTTP Request Message`의 Header 부분에 url 이 담겨서 전송된다. 때문에 url 상에 `?` 뒤에 데이터가 붙어 request 를 보내게 되는 것이다. 이러한 방식은 url 이라는 공간에 담겨가기 때문에 전송할 수 있는 데이터의 크기가 제한적이다. 또 보안이 필요한 데이터에 대해서는 데이터가 그대로 url 에 노출되므로 `GET`방식은 적절하지 않다.

## POST 방식

POST 방식의 request 는 `HTTP Request Message`의 Body 부분에 데이터가 담겨서 전송된다. 때문에 바이너리 데이터를 요청하는 경우 POST 방식으로 보내야 하는 것처럼 데이터 크기가 GET 방식보다 크고 보안면에서 낫다.

# 2. TCP vs UDP

### UDP

`UDP(User Datagram Protocol, 사용자 데이터그램 프로토콜)`는 **비연결형 프로토콜** 이다. IP 데이터그램을 캡슐화하여 보내는 방법과 연결 설정을 하지 않고 보내는 방법을 제공

예) DNS, Broadcasting (도메인, 실시간 동영상 서비스에서 사용)

-   혼잡제어X, 흐름제어X
-   비신뢰성(데이터 재전송 X)
-   일대일 통신, 다대다 통신, 일대다 통신

### TCP

`TCP(Transmission Control Protocol, 전송 제어 프로토콜)`는 **연결형 프로토콜** 이다. IP 데이터그램을 캡슐화하여 보내는 방법과 연결 설정을 하지 않고 보내는 방법을 제공

예) HTTP, Email, File transfer

-   혼잡제어, 흐름제어
-   신뢰성 보장(데이터 재전송 존재)
-   전이중 : 전송이 양방향으로 동시에 일어남
-   점대점 : 연결이 정확히 2개의 종단점을 가짐
-   3-way-handshaking
-   4-way-handshaking

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fd1b8b6d-376f-46cb-9f58-d31481d1c268/Untitled.png)

3-way-handshaking, 4-way-handshaking을 설명할줄 알아야함, TCP, UDP 차이를 설명할줄 알아야함

## 4. HTTP VS HTTPS

### 문제점 1.

**통신 상대를 확인하지 않기 때문에 위장이 가능하다.**

→

-   `SSL`로은 제 3자 기관에 의해 발행되는 것이기 때문에 서버나 클라이언트가 실재하는 사실을 증명
-   클라이언트는 이 증명서로 본인 확인을 하고 웹 사이트 인증에서도 이용할 수 있다.

### 문제점 2.

**완전성을 증명할 수 없기 때문에 변조가 가능하다**

-   서버 또는 클라이언트에서 수신한 내용이 송신측에서 보낸 내용과 일치한다라는 것을 보장할 수 없는 것
-   중간자 공격(Man-in-the-Middle)을 진행하더라도 이 사실을 알 수 없다.
    -   중간자 공격 : 같이 공격자가 도중에 리퀘스트나 리스폰스를 빼앗아 변조하는 공격

→ SSL로 해결

### HTTPS

HTTP에 암호화와 인증, 그리고 완전성 보호를 더한 HTTPS

참고

-   공개키 암호화 : 공개키로 암호화를 하면 개인키로만 복호화
    -   개인키는 나만 가지고 있으므로, 나만 볼 수 있다.
-   개인키 암호화 : 개인키로 암호화하면 공개키로만 복호화
    -   공개키는 모두에게 공개되어 있으므로, 내가 인증한 정보임을 알려 신뢰성을 보장할 수 있다.

**HTTPS의 동작 과정**

1. A기업은 공개키/개인키를 발급
2. CA(Certificate Authority)에게 공개키를 저장하는 인증서 발급 요청
3. CA는 CA의 이름, 서버의 공개키, 서버의 정보를 기반으로 인증서를 생성 후 CA 개인키로 암호화하여 A 기업에게 인증서 제공
4. A기업은 클라이언트에게 암호화된 인증서 제공
5. 클라이언트는 CA의 공개키를 통해 인증서를 복호화
6. 암호화된 인증서를 복호화하여 얻은 A기업의 공개키로 데이터를 암호화하여 요청을 전송

호화된 인증서는 CA의 개인키로 암호화되었기 때문에, 신뢰성을 확보할 수 있고, 클라이언트는 A 기업의 공개키로 데이터를 암호화하였기 때문에 A기업만 복호화하여 원본의 데이터를 얻을 수 있다.

정리하면

공개키 암호화 방식의 장점 : 키를 전달하는데 쉬움

대칭키 암호화 방식의 장점 : 암호화와 복호화가 쉬움

두가지 장점을 섞어서 통신

## 5. HTTP 1.1 vs HTTP 2.0

HTTP 1.1 이 느린 이유

-   HOL(Head Of Line) Blocking (특정 응답 지연)
    -   Request의 순서와 Response의 응답순서는 동기화
-   RTT(Round Trip TIme) 증가 (양방향 지연)
-   헤더가 크다 (특히 쿠키때문에) - 매 요청마다 중복되는 헤더를 보내게 되기 때문에 비효율적

### HTTP/1.1의 속도 문제를 개선하기 위한 노력

-   이미지 스프라이트 - 다수의 리소스 요청을 보내게되면 HOC Blocking이 발생할 수도 있기 때문에 이미지들을 하나로 합쳐서 리소스 요청을 한 번만 보내는 방식
-   CSS/JavaScript 압축

### HTTP/2.0

HTTP/2.0은 새로운 기능이 도입되기 보단 HTTP/1.1의 성능을 개선시키는데 많은 노력을 쏟았다. 즉, 성능 향상에 초점을 맞춘 프로토콜이다.

**Multiplexed Streams**

한 커넥션에서 여러개의 메세지를 주고받을 수 있으며, 응답은 순서에 상관없이 stream으로 주고 받는다

**Header Compression**

Header의 내용과 중복되는 필드를 재전송 하지 않도록 하여, 데이터를 절약한다. 또한 기존에 HTTP Header가 Plain Text(평문)이었지만, HTTP/2에서는 Hash Table과 Huffman Coding을 사용하는 HPACK이라는 Header 압축방식을 이용하여 데이터 전송 효율을 높였다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6279b153-f33f-4f47-bc93-4b2e54b4e5c3/Untitled.png)

## 6. REST API 란?

Representational State Transfer API(Application Programming Interface)

**API는** 응용 프로그램(애플리케이션)에서 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스를 뜻합니다. 주로 파일 제어, 창 제어, 화상 처리, 문자 제어 등을 위한 인터페이스를 제공합니다

`애플리케이션`과 `운영체제` 그리고 `애플리케이션`과 `프로그래밍 언어가 제공하는 기능` 사이의 **'상호 작용'**을 도와줍니다.

REST(Representational State Transfer)의 약자로 자원을 이름으로 구분하여 해당 자원의 상태를 주고받는 모든 것을 의미합니다.

### **즉 REST란**

1. HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고,
2. HTTP Method(POST, GET, PUT, DELETE)를 통해
3. 해당 자원(URI)에 대한 CRUD Operation을 적용하는 것을 의미합니다.

4. **자원(Resource) : HTTP URI**
5. **자원에 대한 행위(Verb) : HTTP Method**
6. **자원에 대한 행위의 내용 (Representations) : HTTP Message Pay Load**

REST API 란?

웹상에서 사용되는 여러 자원(resource)를 **HTTP URI로 표현**하고, 해당 리소스에 대한 행위를 **HTTP Method로 정의**하는 **방식**

## URI(uniform resource identifier, )

웹 서버의 리소스들은 각자 이름을 가지고 있어서 클라이언트가 원하는 리소스를 지목해서 요청(request)할 수 있습니다. 서버 리소스 이름은 **URI**로 불리며 URI는 인터넷의 우편 주소 같은 것으로 정소 리소스를 고유하게 식별하고 위치를 지정 할 수 있습니다.

## URL(uniform resource locator)

URL은 특정 서버의 어떤 리소스에 대한 구체적인 위치를 표기합니다.예를들어 다음의 URL은 파이썬 로고의 URL인데 파이썬 로고가 정확히 어디에 있는지 어떻게 접근해야 하는지 알려줍니다

## URN(uniform resource name)

URN은 콘텐츠를 이루는 어떤 리소스에 대해서 해당 리소스가 위치에 영향을 받지 않는 유일한 이름 갖는 역할을 합니다.쉽게 말해서 URN은 리소스가 이름을 바꾸지 않는한 이곳저곳으로 옮기더라고 문제없이 작동함을 뜻합니다.

장점 : RESTful API는 그 자체만으로도 API의 목적이 무엇인지 쉽게 알 수 있습니다.

## 7. OSI(Open Systems Interconnection) 7계층이란?

개방형 시스템

### 물리 계층(Physical Layer)

하드웨어 전송 기술

-   아날로그 신호(주파수)를 디지털 신호로 변경해주는 역할
-   전기적인, 기계적인 신호를 주고받는 역할을 하는 계층
-   데이터의 종류나 오류를 제어하지 않는다.

예) 통신 케이블, 허브, 리피터

### 데이터 링크 계층(Data Link Layer)

-   point to point 간의 신뢰성 있는 전송을 보장하기 위한 계층

예) 스위치, 브릿지

### 네트워크 계층(Network Layer)

-   네트워크 계층은 우리가 흔히 아는 IP주소를 제공하는 계층
-   대표적으로 노드들을 거칠때마다 라우팅 해주는 역할

### 전송 계층(Transport Layer)

-   양끝단(End to End)의 사용자들이 데이터를 주고 받을 수 있게 하는 계층
-   TCP, UDP 프로토콜이 있는 계층

TCP, UDP 설명

### 세션 계층(Session Layer)

-   각 프로그램의 **네트워크 통신 상태 관리**와 **동기화**
-   데이터를 만들어 내는 계층
-   양 끝단의 응용 프로세스가 통신을 관리하기 위한 방법을 제공한다.
-   동시 송수신 방식(duplex), 반이중 방식(half-duplex), 전이중 방식(Full-dupelx)

예) RPC, Socket, SSH, TLS

### 표현 계층(Presentation Layer)

-   코드 간의 번역으 담당하여 사용자 시스템에서 데이터의 형식상 차이를 다루는 부담을 응용 계층으로부터 덜어준다.
-   인코딩및 디코딩, 암호화, 복호화 등의 동작이 이루어짐

### 응용 계층(Application Layer)

-   응용 계층은 응용 프로세스와 직접 관계하여 일반적인 응용 서비스를 수행한다.
-   HTTP, FTP 프로토콜이 속함
