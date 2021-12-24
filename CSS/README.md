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

### **브라우저 별로 스타일이 다른 문제를 어떤 접근 방법으로 해결하나요?**

---

-   Reset CSS 또는 Normalize.css를 사용한다. 혹은 Bootstrap 같은 `CSS Framework`를 사용한다. 아니면 autoprefixer를 사용하여 벤더 프리픽스를 코드에 자동으로 추가한다.

### **z-index와 스택 컨텍스트는 어떻게 형성되나요?**

---

-   z-index는 겹치는 요소의 쌓임 순서를 정해주며, 이는 position이 static이 아닌 값을 갖는 요소에 적용된다. 만약 z-index가 지정되지 않으면 DOM에 나타나는 순서대로 요소가 쌓이게 된다.
-   스택 컨텍스트는 레이어들을 포함하는 요소로, 지역 컨택스트 내에서, 자식의 z-index 값은 문서 루트가 아닌 해당 요소를 기준으로 설정된다. 해당 컨텍스트 외부 레이어는 그 사이의 레이어에 올 수 없습니다. 요소 B가 요소 A의 상단에 위치하는 경우, 요소 A의 하위 요소 C는 요소 C가 요소 B보다 z-index가 더 높은 경우에도 요소 B보다 위에 올 수 없습니다.

### **BFC(Block Formatting Context)와 그 작동 방식을 설명하세요.**

---

-   BFC는 블록 박스가 배치된 웹 페이지의 시각적 CSS 렌더링의 일부입니다. float, absolute로 배치된 요소, inline-blocks, table-cells, table-caption 그리고 visible이 아닌 overflow가 있는 요소들이 BFC를 만든다.
-   BFC는 다음 조건 중 하나 이상을 충족시키는 HTML 박스입니다.
    1. `float` 값이 `none`이 아님.
    2. `position`의 값이 `static`도 아니고 `relative`도 아님.
    3. `display`의 값이 `table-cell`, `table-caption`, `inline-block`, `flex`, `inline-flex`임.
    4. `overflow`의 값이 `visible`이 아님.
-   BFC에서 각 박스의 왼쪽 바깥 모서리는 포함하는 블록의 왼쪽 모서리에 닿습니다.
-   BFC collapse 시, 인접한 블록 레벨 박스 사이의 수직 마진이 발생합니다.

### **SVG 스타일링은 무엇이며, 익숙하신가요?**

---

-   네, SVG는 대부분 inline CSS, CSS section 삽입, 외부 CSS file처럼 shape의 색상을 정하는 여러 방법이 있습니다. 웹에서 볼 수 있는 대부분의 SVG는 inline CSS를 사용하지만, 각각 장단점이 있습니다.
-   기본적인 채색은 노드에 `fill`과 `stroke` 두 속성을 설정하여 정할 수 있습니다. `fill`은 객체 안쪽 색을 설정하고 `stroke`는 객체 주의에 그려지는 선의 색을 설정한다. 색상 이름, RGB 값, 16진수 값, RGBA 값 등 HTML에서 사용하는 것과 동일한 CSS 색상 이름 스킴을 사용할 수 있습니다.

```
<rect
  x="10"
  y="10"
  width="100"
  height="100"
  stroke="blue"
  fill="purple"
  fill-opacity="0.5"
  stroke-opacity="0.8"
/>
```

### **Flexbox나 Grid 스펙을 사용해본 적이 있나요?**

---

-   네, Flexbox는 주로 1차원 레이아웃을 대상으로 하며, Grid는 2차원 레이아웃을 대상으로 합니다.
-   Flexbox는 CSS에서 컨테이너 안에 있는 요소의 수직 가운데정렬, sticky footer 등과 같은 많은 일반적인 문제들을 해결합니다. Bootstrap과 Bulma는 Flexbox를 기반으로 하고, 이는 요즘 레이아웃을 만드는 데 권장되는 방법일 것입니다.
-   Grid는 그리드 기반의 레이아웃을 생성하기 위한 가장 직관적인 접근법이며, 현재 ie를 제외한 모든 브라우저에서 Grid 관련 대다수의 기능들을 지원하고 있습니다.

### **반응형 웹사이트를 코딩하는 것과 모바일 우선 전략을 사용하는 것 사이의 차이점을 설명해보세요.**

---

-   우선 이 두가지 접근법은 배타적이지 않습니다. 반응형 웹사이트를 만드는 것은 일부 요소가 미디어 쿼리를 통해 장치의 화면 크기(일반적으로 뷰포트 너비)에 따라 크기나 다른 기능을 조정하도록 반응함을 의미합니다. (ex: 작은 디바이스에서 글꼴 크기를 줄임)
    ```
    @media (min-width: 601px) {
        .my-class {
            font-size: 24px;
        }
    }
    @media (max-width: 600px) {
        .my-class {
            font-size: 12px;
        }
    }
    ```
-   모바일 우선 전략 또한 반응적이지만, 모바일 장치에 대한 모든 스타일을 정의해야하며 나중에 다른 장치에 대한 특정 규칙을 추가합니다.
    ```
    .my-class {
        font-size: 12px;
    }
    @media (min-width: 600px) {
        .my-class {
            font-size: 24px;
        }
    }
    ```
-   해당 방식의 장점은 다음과 같습니다. 모바일 장치에서 적용되는 모든 규칙이 미디어 쿼리에 대해 유효성 검사를 받을 필요가 없으므로 모바일 장치에서 더 뛰어난 성능을 발휘합니다.
-   반응형 CSS 규칙과 관련하여 보다 명확한 코드를 작성해야합니다.
