## Array vs Linked List

### Array

가장 기본적인 자료구조인 `Array` 자료구조는, 논리적 저장 순서와 물리적 저장 순서가 일치한다. 따라서 `인덱스`(index)로 해당 원소(element)에 접근할 수 있다. 그렇기 때문에 찾고자 하는 원소의 인덱스 값을 알고 있으면 `Big-O(1)`에 해당 원소로 접근할 수 있다. 즉 **random access** 가 가능하다는 장점이 있는 것이다.

하지만 삭제 또는 삽입의 과정에서는 해당 원소에 접근하여 작업을 완료한 뒤(O(1)), 또 한 가지의 작업을 추가적으로 해줘야 하기 때문에, 시간이 더 걸린다. 만약 배열의 원소 중 어느 원소를 삭제했다고 했을 때, 배열의 연속적인 특징이 깨지게 된다. 즉 빈 공간이 생기는 것이다. 따라서 삭제한 원소보다 큰 인덱스를 갖는 원소들을 `shift`해줘야 하는 비용(cost)이 발생하고 이 경우의 시간 복잡도는 O(n)가 된다. 그렇기 때문에 Array 자료구조에서 삭제 기능에 대한 time complexity 의 worst case 는 O(n)이 된다.

삽입의 경우도 마찬가지이다. 만약 첫번째 자리에 새로운 원소를 추가하고자 한다면 모든 원소들의 인덱스를 1 씩 shift 해줘야 하므로 이 경우도 O(n)의 시간을 요구하게 된다.

### Linked List

이 부분에 대한 문제점을 해결하기 위한 자료구조가 linked list 이다. 각각의 원소들은 자기 자신 다음에 어떤 원소인지만을 기억하고 있다. 따라서 이 부분만 다른 값으로 바꿔주면 삭제와 삽입을 O(1) 만에 해결할 수 있는 것이다.

하지만 Linked List 역시 한 가지 문제가 있다. 원하는 위치에 삽입을 하고자 하면 원하는 위치를 Search 과정에 있어서 첫번째 원소부터 다 확인해봐야 한다는 것이다. Array 와는 달리 논리적 저장 순서와 물리적 저장 순서가 일치하지 않기 때문이다. 이것은 일단 삽입하고 정렬하는 것과 마찬가지이다. 이 과정 때문에, 어떠한 원소를 삭제 또는 추가하고자 했을 때, 그 원소를 찾기 위해서 O(n)의 시간이 추가적으로 발생하게 된다.

결국 linked list 자료구조는 search 에도 O(n)의 time complexity 를 갖고, 삽입, 삭제에 대해서도 O(n)의 time complexity 를 갖는다. 그렇다고 해서 아주 쓸모없는 자료구조는 아니기에, 우리가 학습하는 것이다. 이 Linked List 는 Tree 구조의 근간이 되는 자료구조이며, Tree 에서 사용되었을 때 그 유용성이 드러난다.

#### Personal Recommendation

-   Array 를 기반으로한 Linked List 구현
-   ArrayList 를 기반으로한 Linked List 구현

---

</br>

## Stack and Queue

### Stack

선형 자료구조의 일종으로 `Last In First Out (LIFO)`. 즉, 나중에 들어간 원소가 먼저 나온다. 이것은 Stack 의 가장 큰 특징이다. 차곡차곡 쌓이는 구조로 먼저 Stack 에 들어가게 된 원소는 맨 바닥에 깔리게 된다. 그렇기 때문에 늦게 들어간 녀석들은 그 위에 쌓이게 되고 호출 시 가장 위에 있는 녀석이 호출되는 구조이다.

### Queue

선형 자료구조의 일종으로 `First In First Out (FIFO)`. 즉, 먼저 들어간 놈이 먼저 나온다. Stack 과는 반대로 먼저 들어간 놈이 맨 앞에서 대기하고 있다가 먼저 나오게 되는 구조이다. 참고로 Java Collection 에서 Queue 는 인터페이스이다. 이를 구현하고 있는 `Priority queue`등을 사용할 수 있다.

#### Personal Recommendation

-   Stack 을 사용하여 미로찾기 구현하기
-   Queue 를 사용하여 Heap 자료구조 구현하기
-   Stack 두 개로 Queue 자료구조 구현하기
-   Stack 으로 괄호 유효성 체크 코드 구현하기

## 스택(Stack)

입력과 출력이 한 곳(방향)으로 제한

##### LIFO (Last In First Out, 후입선출) : 가장 나중에 들어온 것이 가장 먼저 나옴

<br>

**_언제 사용?_**

함수의 콜스택, 문자열 역순 출력, 연산자 후위표기법

<br>

데이터 넣음 : push()

데이터 최상위 값 뺌 : pop()

비어있는 지 확인 : isEmpty()

꽉차있는 지 확인 : isFull()

+SP

<br>

push와 pop할 때는 해당 위치를 알고 있어야 하므로 기억하고 있는 '스택 포인터(SP)'가 필요함

스택 포인터는 다음 값이 들어갈 위치를 가리키고 있음 (처음 기본값은 -1)

```java
private int sp = -1;
```

<br>

##### push

```java
public void push(Object o) {
    if(isFull(o)) {
        return;
    }

    stack[++sp] = o;
}
```

스택 포인터가 최대 크기와 같으면 return

아니면 스택의 최상위 위치에 값을 넣음

<br>

##### pop

```java
public Object pop() {

    if(isEmpty(sp)) {
        return null;
    }

    Object o = stack[sp--];
    return o;

}
```

스택 포인터가 0이 되면 null로 return;

아니면 스택의 최상위 위치 값을 꺼내옴

<br>

##### isEmpty

```java
private boolean isEmpty(int cnt) {
    return sp == -1 ? true : false;
}
```

입력 값이 최초 값과 같다면 true, 아니면 false

<br>

##### isFull

```java
private boolean isFull(int cnt) {
    return sp + 1 == MAX_SIZE ? true : false;
}
```

스택 포인터 값+1이 MAX_SIZE와 같으면 true, 아니면 false

<br>

<br>

#### 동적 배열 스택

위처럼 구현하면 스택에는 MAX_SIZE라는 최대 크기가 존재해야 한다

(스택 포인터와 MAX_SIZE를 비교해서 isFull 메소드로 비교해야되기 때문!)

<br>

최대 크기가 없는 스택을 만드려면?

> arraycopy를 활용한 동적배열 사용

<br>

```java
public void push(Object o) {

    if(isFull(sp)) {

        Object[] arr = new Object[MAX_SIZE * 2];
        System.arraycopy(stack, 0, arr, 0, MAX_SIZE);
        stack = arr;
        MAX_SIZE *= 2; // 2배로 증가
    }

    stack[sp++] = o;
}
```

기존 스택의 2배 크기만큼 임시 배열(arr)을 만들고

arraycopy를 통해 stack의 인덱스 0부터 MAX_SIZE만큼을 arr 배열의 0번째부터 복사한다

복사 후에 arr의 참조값을 stack에 덮어씌운다

마지막으로 MAX_SIZE의 값을 2배로 증가시켜주면 된다.

<br>

이러면, 스택이 가득찼을 때 자동으로 확장되는 스택을 구현할 수 있음

<br>

#### 스택을 연결리스트로 구현해도 해결 가능

```java
public class Node {

    public int data;
    public Node next;

    public Node() {
    }

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```

```java
public class Stack {
    private Node head;
    private Node top;

    public Stack() {
        head = top = null;
    }

    private Node createNode(int data) {
        return new Node(data);
    }

    private boolean isEmpty() {
        return top == null ? true : false;
    }

    public void push(int data) {
        if (isEmpty()) { // 스택이 비어있다면
            head = createNode(data);
            top = head;
        }
        else { //스택이 비어있지 않다면 마지막 위치를 찾아 새 노드를 연결시킨다.
            Node pointer = head;

            while (pointer.next != null)
                pointer = pointer.next;

            pointer.next = createNode(data);
            top = pointer.next;
        }
    }

    public int pop() {
        int popData;
        if (!isEmpty()) { // 스택이 비어있지 않다면!! => 데이터가 있다면!!
            popData = top.data; // pop될 데이터를 미리 받아놓는다.
            Node pointer = head; // 현재 위치를 확인할 임시 노드 포인터

            if (head == top) // 데이터가 하나라면
                head = top = null;
            else { // 데이터가 2개 이상이라면
                while (pointer.next != top) // top을 가리키는 노드를 찾는다.
                    pointer = pointer.next;

                pointer.next = null; // 마지막 노드의 연결을 끊는다.
                top = pointer; // top을 이동시킨다.
            }
            return popData;
        }
        return -1; // -1은 데이터가 없다는 의미로 지정해둠.

    }

}
```

<br>

<br>

<br>

## 큐(Queue)

입력과 출력을 한 쪽 끝(front, rear)으로 제한

##### FIFO (First In First Out, 선입선출) : 가장 먼저 들어온 것이 가장 먼저 나옴

<br>

**_언제 사용?_**

버퍼, 마구 입력된 것을 처리하지 못하고 있는 상황, BFS

<br>

큐의 가장 첫 원소를 front, 끝 원소를 rear라고 부름

큐는 **들어올 때 rear로 들어오지만, 나올 때는 front부터 빠지는 특성**을 가짐

접근방법은 가장 첫 원소와 끝 원소로만 가능

<br>

데이터 넣음 : enQueue()

데이터 뺌 : deQueue()

비어있는 지 확인 : isEmpty()

꽉차있는 지 확인 : isFull()

<br>

데이터를 넣고 뺄 때 해당 값의 위치를 기억해야 함. (스택에서 스택 포인터와 같은 역할)

이 위치를 기억하고 있는 게 front와 rear

front : deQueue 할 위치 기억

rear : enQueue 할 위치 기억

<br>

##### 기본값

```java
private int size = 0;
private int rear = -1;
private int front = -1;

Queue(int size) {
    this.size = size;
    this.queue = new Object[size];
}
```

<br>

<br>

##### enQueue

```java
public void enQueue(Object o) {

    if(isFull()) {
        return;
    }

    queue[++rear] = o;
}
```

enQueue 시, 가득 찼다면 꽉 차 있는 상태에서 enQueue를 했기 때문에 overflow

아니면 rear에 값 넣고 1 증가

<br>

<br>

##### deQueue

```java
public Object deQueue(Object o) {

    if(isEmpty()) {
        return null;
    }

    Object o = queue[front];
    queue[front++] = null;
    return o;
}
```

deQueue를 할 때 공백이면 underflow

front에 위치한 값을 object에 꺼낸 후, 꺼낸 위치는 null로 채워줌

<br>

##### isEmpty

```java
public boolean isEmpty() {
    return front == rear;
}
```

front와 rear가 같아지면 비어진 것

<br>

##### isFull

```java
public boolean isFull() {
    return (rear == queueSize-1);
}
```

rear가 사이즈-1과 같아지면 가득찬 것

<br>

---

일반 큐의 단점 : 큐에 빈 메모리가 남아 있어도, 꽉 차있는것으로 판단할 수도 있음

(rear가 끝에 도달했을 때)

<br>

이를 개선한 것이 **'원형 큐'**

논리적으로 배열의 처음과 끝이 연결되어 있는 것으로 간주함!

<br>

원형 큐는 초기 공백 상태일 때 front와 rear가 0

공백, 포화 상태를 쉽게 구분하기 위해 **자리 하나를 항상 비워둠**

```
(index + 1) % size로 순환시킨다
```

<br>

##### 기본값

```java
private int size = 0;
private int rear = 0;
private int front = 0;

Queue(int size) {
    this.size = size;
    this.queue = new Object[size];
}
```

<br>

##### enQueue

```java
public void enQueue(Object o) {

    if(isFull()) {
        return;
    }

    rear = (++rear) % size;
    queue[rear] = o;
}
```

enQueue 시, 가득 찼다면 꽉 차 있는 상태에서 enQueue를 했기 때문에 overflow

<br>

<br>

##### deQueue

```java
public Object deQueue(Object o) {

    if(isEmpty()) {
        return null;
    }

    front = (++front) % size;
    Object o = queue[front];
    return o;
}
```

deQueue를 할 때 공백이면 underflow

<br>

##### isEmpty

```java
public boolean isEmpty() {
    return front == rear;
}
```

front와 rear가 같아지면 비어진 것

<br>

##### isFull

```java
public boolean isFull() {
    return ((rear+1) % size == front);
}
```

rear+1%size가 front와 같으면 가득찬 것

<br>

원형 큐의 단점 : 메모리 공간은 잘 활용하지만, 배열로 구현되어 있기 때문에 큐의 크기가 제한

<br>

<br>

이를 개선한 것이 '연결리스트 큐'

##### 연결리스트 큐는 크기가 제한이 없고 삽입, 삭제가 편리

<br>

##### enqueue 구현

```java
public void enqueue(E item) {
    Node oldlast = tail; // 기존의 tail 임시 저장
    tail = new Node; // 새로운 tail 생성
    tail.item = item;
    tail.next = null;
    if(isEmpty()) head = tail; // 큐가 비어있으면 head와 tail 모두 같은 노드 가리킴
    else oldlast.next = tail; // 비어있지 않으면 기존 tail의 next = 새로운 tail로 설정
}
```

> -   데이터 추가는 끝 부분인 tail에 한다.
>
> -   기존의 tail는 보관하고, 새로운 tail 생성
>
> -   큐가 비었으면 head = tail를 통해 둘이 같은 노드를 가리키도록 한다.
> -   큐가 비어있지 않으면, 기존 tail의 next에 새로만든 tail를 설정해준다.

<br>

##### dequeue 구현

```java
public T dequeue() {
    // 비어있으면
    if(isEmpty()) {
        tail = head;
        return null;
    }
    // 비어있지 않으면
    else {
        T item = head.item; // 빼낼 현재 front 값 저장
        head = head.next; // front를 다음 노드로 설정
        return item;
    }
}
```

> -   데이터는 head로부터 꺼낸다. (가장 먼저 들어온 것부터 빼야하므로)
> -   head의 데이터를 미리 저장해둔다.
> -   기존의 head를 그 다음 노드의 head로 설정한다.
> -   저장해둔 데이터를 return 해서 값을 빼온다.

<br>

이처럼 삽입은 tail, 제거는 head로 하면서 삽입/삭제를 스택처럼 O(1)에 가능하도록 구현이 가능하다.

---

</br>

## Tree

트리는 스택이나 큐와 같은 선형 구조가 아닌 비선형 자료구조이다. 트리는 계층적 관계(Hierarchical Relationship)을 표현하는 자료구조이다. 이 `트리`라는 자료구조는 표현에 집중한다. 무엇인가를 저장하고 꺼내야 한다는 사고에서 벗어나 트리라는 자료구조를 바라보자.

#### 트리를 구성하고 있는 구성요소들(용어)

-   Node (노드) : 트리를 구성하고 있는 각각의 요소를 의미한다.
-   Edge (간선) : 트리를 구성하기 위해 노드와 노드를 연결하는 선을 의미한다.
-   Root Node (루트 노드) : 트리 구조에서 최상위에 있는 노드를 의미한다.
-   Terminal Node ( = leaf Node, 단말 노드) : 하위에 다른 노드가 연결되어 있지 않은 노드를 의미한다.
-   Internal Node (내부노드, 비단말 노드) : 단말 노드를 제외한 모든 노드로 루트 노드를 포함한다.

</br>

### Binary Tree (이진 트리)

루트 노드를 중심으로 두 개의 서브 트리(큰 트리에 속하는 작은 트리)로 나뉘어 진다. 또한 나뉘어진 두 서브 트리도 모두 이진 트리어야 한다. 재귀적인 정의라 맞는듯 하면서도 이해가 쉽지 않을 듯하다. 한 가지 덧붙이자면 공집합도 이진 트리로 포함시켜야 한다. 그래야 재귀적으로 조건을 확인해갔을 때, leaf node 에 다다랐을 때, 정의가 만족되기 때문이다. 자연스럽게 노드가 하나 뿐인 것도 이진 트리 정의에 만족하게 된다.

트리에서는 각 `층별로` 숫자를 매겨서 이를 트리의 `Level(레벨)`이라고 한다. 레벨의 값은 0 부터 시작하고 따라서 루트 노드의 레벨은 0 이다. 그리고 트리의 최고 레벨을 가리켜 해당 트리의 `height(높이)`라고 한다.

#### Perfect Binary Tree (포화 이진 트리), Complete Binary Tree (완전 이진 트리), Full Binary Tree (정 이진 트리)

모든 레벨이 꽉 찬 이진 트리를 가리켜 포화 이진 트리라고 한다. 위에서 아래로, 왼쪽에서 오른쪽으로 순서대로 차곡차곡 채워진 이진 트리를 가리켜 완전 이진 트리라고 한다. 모든 노드가 0개 혹은 2개의 자식 노드만을 갖는 이진 트리를 가리켜 정 이진 트리라고 한다. 배열로 구성된 `Binary Tree`는 노드의 개수가 n 개이고 root가 0이 아닌 1에서 시작할 때, i 번째 노드에 대해서 parent(i) = i/2 , left_child(i) = 2i , right_child(i) = 2i + 1 의 index 값을 갖는다.

</br>

### BST (Binary Search Tree)

효율적인 탐색을 위해서는 어떻게 찾을까만 고민해서는 안된다. 그보다는 효율적인 탐색을 위한 저장방법이 무엇일까를 고민해야 한다. 이진 탐색 트리는 이진 트리의 일종이다. 단 이진 탐색 트리에는 데이터를 저장하는 규칙이 있다. 그리고 그 규칙은 특정 데이터의 위치를 찾는데 사용할 수 있다.

-   규칙 1. 이진 탐색 트리의 노드에 저장된 키는 유일하다.
-   규칙 2. 부모의 키가 왼쪽 자식 노드의 키보다 크다.
-   규칙 3. 부모의 키가 오른쪽 자식 노드의 키보다 작다.
-   규칙 4. 왼쪽과 오른쪽 서브트리도 이진 탐색 트리이다.

이진 탐색 트리의 탐색 연산은 O(log n)의 시간 복잡도를 갖는다. 사실 정확히 말하면 O(h)라고 표현하는 것이 맞다. 트리의 높이를 하나씩 더해갈수록 추가할 수 있는 노드의 수가 두 배씩 증가하기 때문이다. 하지만 이러한 이진 탐색 트리는 Skewed Tree(편향 트리)가 될 수 있다. 저장 순서에 따라 계속 한 쪽으로만 노드가 추가되는 경우가 발생하기 때문이다. 이럴 경우 성능에 영향을 미치게 되며, 탐색의 Worst Case 가 되고 시간 복잡도는 O(n)이 된다.

배열보다 많은 메모리를 사용하며 데이터를 저장했지만 탐색에 필요한 시간 복잡도가 같게 되는 비효율적인 상황이 발생한다. 이를 해결하기 위해 `Rebalancing` 기법이 등장하였다. 균형을 잡기 위한 트리 구조의 재조정을 `Rebalancing`이라 한다. 이 기법을 구현한 트리에는 여러 종류가 존재하는데 그 중에서 하나가 뒤에서 살펴볼 `Red-Black Tree`이다.

#### Personal Recommendation

-   Binary Search Tree 구현하기
-   주어진 트리가 Binary 트리인지 확인하는 알고리즘 구현하기

## Graph

### 정점과 간선의 집합, Graph

_cf) 트리 또한 그래프이며, 그 중 사이클이 허용되지 않는 그래프를 말한다._

### 그래프 관련 용어 정리

#### Undirected Graph 와 Directed Graph (Digraph)

말 그대로 정점과 간선의 연결관계에 있어서 방향성이 없는 그래프를 Undirected Graph 라 하고,
간선에 방향성이 포함되어 있는 그래프를 Directed Graph 라고 한다.

-   Directed Graph (Digraph)

```
V = {1, 2, 3, 4, 5, 6}
E = {(1, 4), (2,1), (3, 4), (3, 4), (5, 6)}
(u, v) = vertex u에서 vertex v로 가는 edge
```

-   Undirected Graph

```
V = {1, 2, 3, 4, 5, 6}
E = {(1, 4), (2,1), (3, 4), (3, 4), (5, 6)}
(u, v) = vertex u와 vertex v를 연결하는 edge
```

#### Degree

Undirected Graph 에서 각 정점(Vertex)에 연결된 Edge 의 개수를 Degree 라 한다.
Directed Graph 에서는 간선에 방향성이 존재하기 때문에 Degree 가 두 개로 나뉘게 된다.
각 정점으로부터 나가는 간선의 개수를 Outdegree 라 하고, 들어오는 간선의 개수를 Indegree 라 한다.

#### 가중치 그래프(Weight Graph)와 부분 그래프(Sub Graph)

가중치 그래프란 간선에 가중치 정보를 두어서 구성한 그래프를 말한다. 반대의 개념인 비가중치 그래프 즉, 모든 간선의 가중치가 동일한 그래프도 물론 존재한다. 부분 집합과 유사한 개념으로 부분 그래프라는 것이 있다. 부분 그래프는 본래의 그래프의 일부 정점 및 간선으로 이루어진 그래프를 말한다.

</br>

### 그래프를 구현하는 두 방법

#### 인접 행렬 (adjacent matrix) : 정방 행렬을 사용하는 방법

해당하는 위치의 value 값을 통해서 vertex 간의 연결 관계를 O(1) 으로 파악할 수 있다. Edge 개수와는 무관하게 V^2 의 Space Complexity 를 갖는다. Dense graph 를 표현할 때 적절할 방법이다.

#### 인접 리스트 (adjacent list) : 연결 리스트를 사용하는 방법

vertex 의 adjacent list 를 확인해봐야 하므로 vertex 간 연결되어있는지 확인하는데 오래 걸린다. Space Complexity 는 O(E + V)이다. Sparse graph 를 표현하는데 적당한 방법이다.

</br>

### 그래프 탐색

그래프는 정점의 구성 뿐만 아니라 간선의 연결에도 규칙이 존재하지 않기 때문에 탐색이 복잡하다. 따라서 그래프의 모든 정점을 탐색하기 위한 방법은 다음의 두 가지 알고리즘을 기반으로 한다.

#### 깊이 우선 탐색 (Depth First Search: DFS)

그래프 상에 존재하는 임의의 한 정점으로부터 연결되어 있는 한 정점으로만 나아간다라는 방법을 우선으로 탐색한다. 일단 연결된 정점으로 탐색하는 것이다. 연결할 수 있는 정점이 있을 때까지 계속 연결하다가 더이상 연결되지 않은 정점이 없으면 바로 그 전 단계의 정점으로 돌아가서 연결할 수 있는 정점이 있는지 살펴봐야 할 것이다. 갔던 길을 되돌아 오는 상황이 존재하는 미로찾기처럼 구성하면 되는 것이다. 어떤 자료구조를 사용해야할까? 바로 Stack 이다.
**Time Complexity : O(V+E) … vertex 개수 + edge 개수**

#### 너비 우선 탐색 (Breadth First Search: BFS)

그래프 상에 존재하는 임의의 한 정점으로부터 연결되어 있는 모든 정점으로 나아간다. Tree 에서의 Level Order Traversal 형식으로 진행되는 것이다. BFS 에서는 자료구조로 Queue 를 사용한다. 연락을 취할 정점의 순서를 기록하기 위한 것이다.
우선, 탐색을 시작하는 정점을 Queue 에 넣는다.(enqueue) 그리고 dequeue 를 하면서 dequeue 하는 정점과 간선으로 연결되어 있는 정점들을 enqueue 한다.
즉 vertex 들을 방문한 순서대로 queue 에 저장하는 방법을 사용하는 것이다.
**Time Complexity : O(V+E) … vertex 개수 + edge 개수**
_**! BFS 로 구한 경로는 최단 경로이다.**_

</br>

### Minimum Spanning Tree

그래프 G 의 spanning tree 중 edge weight 의 합이 최소인 `spanning tree`를 말한다. 여기서 말하는 `spanning tree`란 그래프 G 의 모든 vertex 가 cycle 이 없이 연결된 형태를 말한다.

### Kruskal Algorithm

초기화 작업으로 **edge 없이** vertex 들만으로 그래프를 구성한다. 그리고 weight 가 제일 작은 edge 부터 검토한다. 그러기 위해선 Edge Set 을 non-decreasing 으로 sorting 해야 한다. 그리고 가장 작은 weight 에 해당하는 edge 를 추가하는데 추가할 때 그래프에 cycle 이 생기지 않는 경우에만 추가한다. spanning tree 가 완성되면 모든 vertex 들이 연결된 상태로 종료가 되고 완성될 수 없는 그래프에 대해서는 모든 edge 에 대해 판단이 이루어지면 종료된다.
[Kruskal Algorithm의 세부 동작과정](https://gmlwjd9405.github.io/2018/08/29/algorithm-kruskal-mst.html)
[Kruskal Algorithm 관련 Code](https://github.com/morecreativa/Algorithm_Practice/blob/master/Kruskal%20Algorithm.cpp)

#### 어떻게 cycle 생성 여부를 판단하는가?

Graph 의 각 vertex 에 `set-id`라는 것을 추가적으로 부여한다. 그리고 초기화 과정에서 모두 1~n 까지의 값으로 각각의 vertex 들을 초기화 한다. 여기서 0 은 어떠한 edge 와도 연결되지 않았음을 의미하게 된다. 그리고 연결할 때마다 `set-id`를 하나로 통일시키는데, 값이 동일한 `set-id` 개수가 많은 `set-id` 값으로 통일시킨다.

#### Time Complexity

1.  Edge 의 weight 를 기준으로 sorting - O(E log E)
2.  cycle 생성 여부를 검사하고 set-id 를 통일 - O(E + V log V)
    => 전체 시간 복잡도 : O(E log E)

### Prim Algorithm

초기화 과정에서 한 개의 vertex 로 이루어진 초기 그래프 A 를 구성한다. 그리고나서 그래프 A 내부에 있는 vertex 로부터 외부에 있는 vertex 사이의 edge 를 연결하는데 그 중 가장 작은 weight 의 edge 를 통해 연결되는 vertex 를 추가한다. 어떤 vertex 건 간에 상관없이 edge 의 weight 를 기준으로 연결하는 것이다. 이렇게 연결된 vertex 는 그래프 A 에 포함된다. 위 과정을 반복하고 모든 vertex 들이 연결되면 종료한다.

#### Time Complexity

=> 전체 시간 복잡도 : O(E log V)

</br>
