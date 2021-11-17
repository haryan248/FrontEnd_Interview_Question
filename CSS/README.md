## CSS

**선택자 우선순위 (= CSS 적용 순서)**

(!important > 인라인 > 아이디 > 클래스 > 요소)

**class와 id의 차이점에 관해서 설명해주세요.**

-   class는 중복 클래스가능
-   id는 중복 아이디 불가능 , 태그에서 중복되는 아이디가 있으면 안된다.
-   id는 한가지 id만 가능하다.

**Floats가 어떻게 동작하는지 설명해주세요.**

-   float 속성을 사용해 박스를 왼쪽(left) 또는 오른쪽(right)으로 "부유"시키는 레이아웃 기법
-   플로팅된 요소는 display: inline-block;을 선언한 것과 동일

**z-index에 관해 설명해주세요.**

-   position 속성이 있어야 z-index 사용이 가능(relative, absolute, fixed)
-   z-index 값을 따로 설정하지 않으면 기본 값은 0

**position에 대해 설명해주세요.**

-   static
    -   차례대로 왼쪽에서 오른쪽, 위에서 아래로 쌓임
-   relative
    -   top(위), right(오른쪽), bottom(아래), left(왼쪽) 속성을 사용해 위치 조절이 가능
    -   각각의 방향을 기준으로 태그 안쪽 방향으로 이동(5px시 아래로 이동)
-   absolute
    -   **position: static 속성을 가지고 있지 않은 조상을 기준**으로 움직
    -   조상 중에 포지션이 relative, absolute, fixed인 태그가 없다면 가장 위의 태그(body)가 기준
-   fixed

**display에 대해 설명해주세요.**

-   none
    -   화면에서 사라집니다. 크기 자체도 차지하지 않습니다!
-   block
    -   일반적으로 설정하지 않아도 **div가 갖게되는 기본값**
    -   width 가 자신의 컨테이너의 100%(**가로 한 줄을 다 차지)**
-   inline
    -   **컨텐츠를 딱 감쌀정도의 크기**
    -   block태그와 다르게 줄바꿈이 되지 않고, 반드시 컨텐츠를 감싸게 되고, 크기를 변화시킬 수 없습니다.
-   inline-block
    -   line속성에서 할 수 없었던 width/height 변경 및 line-height를 커스텀하게 적용할 수 있는 특징

flex 에 대해 설명해주세요.

grid는 사용해보셨나요?

box model이란 무엇인가요?

margin, padding의 차이는 무엇인가요?

**reset.css, nomalize.css는 무엇인가요?**

-   브라우저별로 각가 태그에 대한 기본 스타일링이 다르기 때문에, 기본적인 것들은 초기화해서 사용
-   reset.css
    -   브라우저에서 통일된 화면을 볼 수 있도록 기본값을 초기화하는 전략
-   nomalize.css
    -   브라우저 간 유저 에이전트 스타일의 오차를 줄이고, 버그만 줄이는 방향으로 스타일을 재지정
    -   웹 브라우저마다 내장되어 있는 기본스타일의 차이를 없애주는 스타일링

CSS를 head 위에 둬야하는 이유는 무엇인가요?

**css box-sizing 속성**

-   content-box
    -   지정한 CSS width 및 height를 컨텐츠 영역에만 적용합니다. border, padding, margin은 따로 계산되어 전체 영역이 설정값보다 커질 수 있습니다.
-   border-box
    -   지정한 CSS width 및 height를 전체 영역에 적용합니다. border, padding, margin을 모두 합산하기 때문에 컨텐츠 영역이 설정값보다 적어질 수 있습니다.

css GRID vs FLEX

### 적응형 vs 반응형

두 방식은 웹 사이트가 모바일 기기와 다양한 화면 크기에서 원활한 정보를 제공하여 더 나은 사용자 경험을 제공하기 위한 방법이라는 것에 공통점이 있습니다.

반응형은 하나의 템플릿으로 모바일, 태블릿, 데스크탑 등 모든 기기에 대응할 수 있는 방식입니다. 반응형은 해상도 별로 보여질 화면을 정의하기 떄문에 초기 기획 단계에서 많은 시간이 듭니다.

적응형은 모바일, 데스크탑 등 각각의 디바이스 별로 독립적인 템플릿을 만들고 각각의 디바이스에 맞는 페이지를 별도 제작후 렌더링 해주는 방식입니다.

반응형은 웹에서 쓰이는 모든 컨텐츠를 다운 받고 현재 해상도에 맞는 화면이 렌더링되기 때문에 로딩 속도가 느리다는 단점이 있습니다.적응형은 디바이스에 맞는 컨텐츠만 다은 받기 때문에 로딩속도가 빠릅니다.