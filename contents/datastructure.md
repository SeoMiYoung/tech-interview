# 1. Data Structure
**:book: Contents**
* [Array](#array)
* [LinkedList](#linkedlist)
* [HashTable](#hashtable)
* [Stack](#stack)
* [Queue](#queue)
* [Graph](#graph)
* [Tree](#tree)
* [Binary Tree](#binary-tree)
* [Binary Search Tree](#binary-search-tree)
* [그래프(Graph)와 트리(Tree)의 차이점](#그래프와-트리의-차이점)
* [Binary Heap](#binary-heap)
* [Red-Black Tree](#red-black-tree)
* [B+ Tree](#b-tree)

---

### Array

> :arrow_double_up:[Top](#1-data-structure)    :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#1-data-structure)    :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)
> - []()

### LinkedList

> :arrow_double_up:[Top](#1-data-structure)    :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#1-data-structure)    :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)
> - []()

### HashTable

* HashTable 개념
  * Key와 Value를 1:1로 연관지어 저장하는 자료구조 (연관배열 구조)
  * Key를 이용하여 Value 도출

* HashTable 기능
  * 연관배열 구조와 동일한 기능 지원
  * Key, Value가 주어졌을 때, 두 값을 저장
  * Key가 주어졌을 때, 해당 Key에 연관된 Value 조회
  * 기존 Key에 새로운 Value가 주어졌을 때, 기존 Value를 새로운 Value로 대체
  * Key가 주어졌을 때, 해당 Key에 연관된 Value 제거

* HashTable 구조

  ![hashtable](./images/hashtable.png)
  * Key, Hash Function, Hash, Value, 저장소(Bucket, Slot)로 구성
  * Key
    * 고유한 값
    * 저장 공간의 효율성을 위해 Hash Function에 입력하여 Hash로 변경 후 저장
      * Key는 길이가 다양하기 때문에 그대로 저장하면 다양한 길이만큼 저장소 구성이 필요
  * Hash Function
    * Key를 Hash로 바꿔주는 역할
    * 해시 충돌(서로 다른 Key가 같은 Hash가 되는 경우)이 발생할 확률을 최대한 줄이는 함수를 만드는 것이 중요
  * Hash
    * Hash Function의 결과
    * 저장소에서 Value와 매칭되어 저장
  * Value
    * 저장소에 최종적으로 저장되는 값
    * 키와 매칭되어 저장, 삭제, 검색, 접근 가능

* HashTable 동작 과정
  1. Key -> Hash Function -> Hash Function 결과 = Hash
  2. Hash를 배열의 Index로 사용
  3. 해당 Index에 Value 저장
  * HashTable 크기가 10이라면 A라는 Key의 Value를 찾을 때 hashFunction("A") % 10 연산을 통해 인덱스 값 계산하여 Value 조회

* Hash 충돌
  * 서로 다른 Key가 Hash Function에서 중복 Hash로 나오는 경우
  * 충돌이 많아질수록 탐색의 시간 복잡도가 O(1)에서 O(n)으로 증가

* Hash 충돌 해결 방법
  > - [[자료구조] Hash 충돌 해결 방법](https://www.youtube.com/watch?v=W-KV24YEB9g&t=997s)
  1. Separating Chaining
      * JDK 내부에서 사용하는 충돌 처리 방식
         * JDK(Java Development Kit)는 자바 애플리케이션을 구축하기 위한 필수적인 플랫폼 구성요소
      * Linked List(데이터 6개 이하) 또는 Red-Black Tree(데이터 8개 이상) 사용
        ![separatingChaining](./images/separatingChaining.png)
         * Linked List는 연산 복잡도가 O(n)이고, Red-Black Tree는 연산 복잡도가 O(log n)이다. 노드 수가 적을 때는 Linked List가 더 효율적이고, 많아지면 Red-Black Tree가 유리합니다. 그래서 기존 노드와 새 노드를 Linked List로 처음에 연결하다가, 노드 수가 8개 이상이 되면 Red-Black Tree로 변환합니다.
      * Linked List 사용 시 충돌이 발생하면 충돌 발생한 인덱스가 가리키고 있는 Linked List에 노드 추가하여 Value 삽입
      * Key에 대한 Value 탐색 시에는 인덱스가 가리키고 있는 Linked List를 선형 검색하여 Value 반환 (삭제도 마찬가지)
      * Linked List 구조를 사용하기 때문에 추가 데이터 수 제약이 적은편
  2. Open addressing
      * 추가 메모리 공간을 사용하지 않고, HashTable 배열의 빈 공간을 사용하는 방법 => 추가 메모리가 필요 없다는게 엄청난 장점임!! 모든 데이터가 테이블내에 저장됨!!
      * Separating Chaining 방식에 비해 적은 메모리 사용
      * 방법은 Linear Probing, Quadratic Probing, Double Hashing
        * Linear Probing(선형 탐사): 충돌 시 순차적으로 다음 버킷을 검사합니다.
          * 1번째 탐색 -> 2번째 탐색 -> 3번째 탐색 -> 4번째 탐색 ...
        * Quadratic Probing(제곱 탐사): 충돌 시 제곱수만큼 떨어진 버킷을 검사합니다.
          * 1번째 탐색 -> 4번째 탐색 -> 9번째 탐색 -> 16번째 탐색 ...
        * Double Hashing(이중 해싱): 두 번째 해시 함수를 사용하여 다음 위치를 결정합니다.
          * 2개의 해시 함수를 사용 (지금까지 한가지의 해시 함수를 사용했지만, 이중해싱은 말 그대로 이중으로 해싱하기 위해 2개의 해시함수가 필요하다.) => 충돌이 발생했으면, 다른 해시함수로 다시 해시값을 만들어낸 후 원소를 검사하는 것이다.
          * 예를 들어서 첫번째 해시 함수는 h(key)로 쓰고, 두번째 해시 함수는 d(key)라고 칭했다고 하자. 두 해시함수는 기본적인 해시함수 h(key)로 키를 인덱스로 변환하고 두 번째 함수 d(key)는 다음 위치를 위한 점프 크기를 다음과 같은 규칙에 따라 정한다.
            * ```(h(key) + j*d(key)) % M, 여기서 j=0,1,2,3...```
  3. Resizing
      * 저장 공간이 일정 수준 채워지면 Separating Chaining의 경우 성능 향을 위해, Open addressing의 경우 배열 크기 확장을 위해 Resizing
      * 보통 두배로 확장
      * 확장 임계점은 현재 데이터 개수가 Hash Bucket 개수의 75%가 될 때
      * 버킷의 사이즈를 늘리자! 그러기 위해서 기존의 버킷을 새로운 버킷에 copy를 하고, 새로운 공간을 만듭니다. 보통 최대 버킷의 max값은 `max(bucket)=2^30`입니다. 

* HashTable 장점
  * 적은 리소스로 많은 데이터를 효율적으로 관리 가능 => 적은 메모리로 많은 데이터를 효율적으로 관리할 수 있음!
    * ex. HDD. Cloud에 있는 많은 데이터를 Hash로 매핑하여 작은 크기의 시 메모리로 프로세스 관리 가능
      * 클라우드에서는 자주 접근하는 데이터(hot data)는 빠른 SSD에, 덜 자주 접근하는 데이터(cold data)는 저렴한 HDD에 저장합니다.
      * HDD나 클라우드는 대용량 데이터 저장을 위한 것이고, 해시 테이블은 이러한 데이터를 효율적으로 관리하고 접근하기 위한 메모리 내 자료구조입니다. 두 개념이 직접적으로 연결되어 있지는 않지만, 대용량 데이터 관리 시스템에서 상호 보완적으로 사용될 수 있습니다.
  * 배열의 인덱스를 사용하기 때문에 빠른 검색, 삽입, 삭제 (O(1))
    * HashTable의 경우 인덱스는 데이터의 고유 위치이기 때문에 삽입 삭제 시 다른 데이터를 이동할 필요가 없어 삽입, 삭제도 빠른 속도 가능
  * Key와 Hash에 연관성이 없어 보안 유리
  * 데이터 캐싱에 많이 사용
    * get(데이터 조회), put(데이터 저장) 기능에 캐시 로직 추가 시 자주 hit하는 데이터 바로 검색 가능
      * 'get'작업 시: 먼저 캐시를 확인하고, 캐시에 없으면 원본 데이터 소스에서 조회합니다.
      * 'put'작업 시: 데이터를 원본 소스에 저장하면서 동시에 캐시에도 저장합니다.
      * '자주 hit하는 데이터'란, 자주 요청되는 데이터를 의미합니다. => 이러한 데이터를 캐시에 저장해 두면, 다음 요청 시 원본 데이터 소스에 접근하지 않고도 빠르게 데이터를 검색할 수 있습니다.
  * 중복 제거 유용
    * 고유한 키 값: 해시 테이블은 각 데이터를 고유한 키와 연관시킵니다. 동일한 키를 가진 데이터를 추가하려고 하면, 기존 데이터를 덮어쓰거나 무시할 수 있어 자연스럽게 중복을 제거할 수 있습니다.
    * 빠른 검색 속도: 해시 테이블은 평균적으로 O(1) 시간 복잡도로 데이터를 검색할 수 있습니다. 이는 새로운 요소를 추가할 때 기존 데이터와의 중복 여부를 빠르게 확인할 수 있게 해줍니다.
    * 효율적인 메모리 사용: 중복된 데이터를 저장하지 않기 때문에, 메모리를 효율적으로 사용할 수 있습니다.

* HashTable 단점
  * 충돌 발생 가능성
  * 공간 복잡도 증가
  * 순서 무시
  * 해시 함수에 의존

* HashTable vs HashMap
  * Key-Value 구조 및 Key에 대한 Hash로 Value 관리하는 것은 동일
  * HashTable
    * 동기
      * 동기화(Synchronized)가 되어있다 => 여러 스레드가 동시에 같은 자원(예: 변수, 객체)에 접근하려 할 때, 한 번에 하나의 스레드만 접근할 수 있도록 제어하는 메커니즘입니다. => 그래서 Tread-safe하다고 하는데, Tread-safe란, 여러 스레드가 동시에 접근해도 프로그램이 의도한 대로 정확하게 동작하는 것을 의미합니다.
    * Key-Value 값으로 null 미허용 (Key가 hashcode(), equals()를 사용하기 때문)
    * 보조 Hash Function과 separating Chaining을 사용해서 비교적 충돌 덜 발생 (Key의 Hash 변형)
  * HashMap
    * 비동기 (멀티 스레드 환경에서 주의)
      * 비동기화되어 있어, 멀티 스레드 환경에서 주의가 필요합니다. 물론, 동기화되지 않아 더 빠르긴 하지만, 멀티스레드 환경에서 안전하지 않을 수 있습니다.
    * Key-Value 값으로 null 허용

* HashTable 성능

    | |평균|최악|
    |----|----|----|
    |탐색|O(1)|O(N)|
    |삽입|O(1)|O(N)|
    |삭제|O(1)|O(N)|

> :arrow_double_up:[Top](#1-data-structure)    :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#1-data-structure)    :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)
> - [Hash, Hashing, Hash Table(해시, 해싱 해시테이블) 자료구조의 이해](https://velog.io/@cyranocoding/Hash-Hashing-Hash-Table%ED%95%B4%EC%8B%9C-%ED%95%B4%EC%8B%B1-%ED%95%B4%EC%8B%9C%ED%85%8C%EC%9D%B4%EB%B8%94-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EC%9D%98-%EC%9D%B4%ED%95%B4-6ijyonph6o)
> - [[자료구조] Hash/HashTable/HashMap](https://hee96-story.tistory.com/48)
> - [[자료구조] 도움많이되는 유튭 영상](https://www.youtube.com/watch?v=ZBu_slSH5Sk)

### Stack
* 스택(Stack)의 개념
    * 약간 엘레베이터 구조라고 이해하면 될 듯 => 엘레베이터 먼저 탄 사람이 가장 구석으로 들어가니깐, 마지막에 들어온 사람이 결국 가장 먼저 내림
      * [암기] 스엘 (스택 엘레베이터)
    * 한 쪽 끝에서만 자료를 넣고 뺄 수 있는 LIFO(Last In First Out) 형식의 자료 구조
* 스택(Stack)의 연산
  * 스택(Stack)는 LIFO(Last In First Out) 를 따른다. 즉, 가장 최근에 스택에 추가한 항목이 가장 먼저 제거될 항목이다.
    * pop(): 스택에서 가장 위에 있는 항목을 제거한다.
    * push(item): item 하나를 스택의 가장 윗 부분에 추가한다.
    * peek(): 스택의 가장 위에 있는 항목을 반환한다.
    * isEmpty(): 스택이 비어 있을 때에 true를 반환한다.
* 스택(Stack)의 사용 사례
  * 우리가 `ctrl + Z`할 때 이런 느낌으로 구현된거임
  * `재귀 알고리즘`을 사용하는 경우 스택이 유용하다.
    * `WHY?` STACK은 LIFO(Last In First Out)특성으로 인해, 가장 마지막에 호출된 함수부터 역순으로 실행이 완료됩니다. 이는 재귀의 기본 케이스(종료 조건)에 도달한 후, 결과가 `역순`으로 전파되는 방식과 일치합니다.
    * 재귀 알고리즘
      * 재귀적으로 함수를 호출해야 하는 경우에 임시 데이터를 스택에 넣어준다.
      * 재귀함수를 빠져 나와 퇴각 검색(backtrack)을 할 때는 스택에 넣어 두었던 임시 데이터를 빼 줘야 한다.
      * 스택은 이런 일련의 행위를 직관적으로 가능하게 해 준다.
      * 또한 스택은 재귀 알고리즘을 반복적 형태(iterative)를 통해서 구현할 수 있게 해준다.
    * 웹 브라우저 방문기록 (뒤로가기)
    * 실행 취소 (undo)
    * 역순 문자열 만들기
    * 수식의 괄호 검사 (연산자 우선순위 표현을 위한 괄호 검사)
      * Ex) 올바른 괄호 문자열(VPS, Valid Parenthesis String) 판단하기
    * 후위 표기법 계산
* 수식의 표기법 - 전위수식(prefix), 후위수식(postfix), 중위수식(infix)
  * 중위수식: 피연산자(숫자) 사이에 연산자(덧셈, 곱셈, 뺄셈, 나눗셈)가 있는 식을 중위식(Infix)라고 합니다. 우리가 보통 알고 있는 수식형태입니다. 하지만, 컴퓨터는 직관적으로 연산자의 우선순위에 따라 연산을 수행할 수 없으므로 연산자 우선순위에 따라 계산해주기 위해 Stack 자료구조를 사용하여 prefix, postfix와 같은 수식으로 변경하여 계산을 해줘야 합니다.
  > - [[Stack] 전위수식(prefix), 후위수식(postfix), 중위수식(infix)](https://injunech.tistory.com/412)
  > - [[연습하는데 직빵인 영상임] 전위표기법 후위표기법 구하기 (Prefix, Postfix)](https://www.youtube.com/watch?v=VZ3twasGCIA)

> :arrow_double_up:[Top](#1-data-structure)    :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#1-data-structure)    :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)
> - [https://gmlwjd9405.github.io/2018/08/03/data-structure-stack.html](https://gmlwjd9405.github.io/2018/08/03/data-structure-stack.html)
> - [스택 유튜브 설명](https://www.youtube.com/watch?v=ELEoJHiqlF4)

### Queue
* 큐(Queue)의 개념
  * 컴퓨터의 기본적인 자료 구조의 한가지로, 먼저 집어 넣은 데이터가 먼저 나오는 FIFO(First In First Out)구조로 저장하는 형식 => 그래서 `순서를 보장`함
* 큐(Queue)의 연산
  * 큐(Queue)는 FIFO(First-In-First-Out) 를 따른다. `(암기: 퍼큐)`
    * add(item): item을 리스트의 끝부분에 추가한다.
    * remove(): 리스트의 첫 번째 항목을 제거한다. => 첫번째 것부터 제거
    * peek(): 큐에서 가장 위에 있는 항목을 반환한다.
    * isEmpty(): 큐가 비어 있을 때에 true를 반환한다.
* 큐(Queue)의 사용 사례
  * 데이터가 `입력된 시간 순서대로 처리해야 할 필요가 있는 상황`에 이용한다.
    * 너비 우선 탐색(BFS, Breadth-First Search) 구현
      * => 깊숙히 있는 것은 후순위임!!
      * 처리해야 할 노드의 리스트를 저장하는 용도로 큐(Queue)를 사용한다.
      * 노드를 하나 처리할 때마다 해당 노드와 인접한 노드들을 큐에 다시 저장한다.
      * 노드를 접근한 순서대로 처리할 수 있다.
    * 캐시(Cache) 구현
    * 우선순위가 같은 작업 예약 (인쇄 대기열)
    * 선입선출이 필요한 대기열 (티켓 카운터)
    * 은행에서 번호표 뽑고 기다리는 순간
    * 콜센터 고객 대기시간
    * 프린터의 출력 처리
    * 윈도우 시스템의 메시지 처리기
    * 프로세스 관리

> :arrow_double_up:[Top](#1-data-structure)    :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#1-data-structure)    :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)
> - [https://gmlwjd9405.github.io/2018/08/02/data-structure-queue.html](https://gmlwjd9405.github.io/2018/08/02/data-structure-queue.html)
> - [큐 유튜브 설명](https://www.youtube.com/watch?v=ZZw6remsJNo)

### Graph
* 그래프(Graph)의 개념
  * 단순히 노드(N, node)와 그 노드를 연결하는 간선(E, edge)을 하나로 모아 놓은 자료 구조
    * 즉, 연결되어 있는 객체 간의 관계를 표현할 수 있는 자료 구조이다.
    * Ex) 지도, 지하철 노선도의 최단 경로, 전기 회로의 소자들, 도로(교차점과 일방 통행길), 선수 과목 등
    * 그래프는 여러 개의 고립된 부분 그래프(Isolated Subgraphs)로 구성될 수 있다.
* 그래프(Graph)의 특징
  * 그래프는 네트워크 모델 이다.
  * 2개 이상의 경로가 가능하다.
    * 즉, 노드들 사이에 무방향/방향에서 양방향 경로를 가질 수 있다.
  * self-loop 뿐 아니라 loop/circuit 모두 가능하다.
    ![image](https://github.com/user-attachments/assets/15d72632-9086-4cb3-8f7d-56fd54eb9bdb)
  * 루트 노드라는 개념이 없다.
  * 부모-자식 관계라는 개념이 없다.
  * 순회는 DFS나 BFS로 이루어진다.
  * 그래프는 순환(Cyclic) 혹은 비순환(Acyclic)이다.
  * 그래프는 크게 방향 그래프와 무방향 그래프가 있다.
  * 간선의 유무는 그래프에 따라 다르다.

> :arrow_double_up:[Top](#1-data-structure)    :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#1-data-structure)    :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)
> - [https://gmlwjd9405.github.io/2018/08/13/data-structure-graph.html](https://gmlwjd9405.github.io/2018/08/13/data-structure-graph.html)
> - [https://ttl-blog.tistory.com/954](https://ttl-blog.tistory.com/954)

### Tree
* 트리(Tree)의 개념
  * 트리는 노드로 이루어진 자료 구조
    1. 트리는 하나의 루트 노드를 갖는다.
    2. 루트 노드는 0개 이상의 자식 노드를 갖고 있다.
    3. 그 자식 노드 또한 0개 이상의 자식 노드를 갖고 있고, 이는 반복적으로 정의된다.
  * 노드(node)들과 노드들을 연결하는 간선(edge)들로 구성되어 있다.
    * ⭐⭐⭐ 트리에는 사이클(cycle)이 존재할 수 없다.
    * 노드들은 특정 순서로 나열될 수도 있고 그럴 수 없을 수도 있다.
    * 각 노드는 부모 노드로의 연결이 있을 수도 있고 없을 수도 있다.
    * 각 노드는 어떤 자료형으로도 표현 가능하다.
  * 비선형 자료구조로 계층적 관계를 표현한다. Ex) 디렉터리 구조, 조직도
  * 그래프의 한 종류
    * 사이클(cycle)이 없는 하나의 연결 그래프(Connected Graph)
    * 또는 `DAG(Directed Acyclic Graph, 방향성이 있는 비순환 그래프)`의 한 종류 이다.
~~~java
class Node {
  public String name;
  public Node[] children;
}
~~~
* 트리(Tree)의 특징
  * 그래프의 한 종류이다. ‘최소 연결 트리’ 라고도 불린다.
  * 트리는 계층 모델 이다.
  * 트리는 DAG(Directed Acyclic Graphs, 방향성이 있는 비순환 그래프)의 한 종류이다.
    * loop나 circuit이 없다. 당연히 self-loop도 없다.
    * 즉, 사이클이 없다.
  * 노드가 N개인 트리는 항상 N-1개의 간선(edge)을 가진다.
    * 즉, 간선은 항상 (정점의 개수 - 1) 만큼을 가진다.
  * 루트에서 어떤 노드로 가는 경로는 유일하다.
    * 임의의 두 노드 간의 경로도 유일하다. 즉, 두 개의 정점 사이에 반드시 1개의 경로만을 가진다.
  * 한 개의 루트 노드만이 존재하며 모든 자식 노드는 한 개의 부모 노드만을 가진다.
    * 부모-자식 관계이므로 흐름은 top-bottom 아니면 bottom-top으로 이루어진다.
  * 순회는 Pre-order, In-order 아니면 Post-order로 이루어진다. 이 3가지 모두 DFS/BFS 안에 있다.
  * 트리는 이진 트리, 이진 탐색 트리, 균형 트리(AVL 트리, red-black 트리), 이진 힙(최대힙, 최소힙) 등이 있다.

> :arrow_double_up:[Top](#1-data-structure)    :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#1-data-structure)    :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)
> - [https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html](https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html)
> - [트리(tree) 구조의 기본 개념과 용어들을 설명합니다~ 이진 트리(binary tree)의 형태에 따른 다양한 종류도 설명하니까요 기본 개념 잡고 싶으시면 도움되실 거에요 :)](https://www.youtube.com/watch?v=ohrwGtqeW-I)

### Binary Tree
<img src="https://github.com/user-attachments/assets/cdb51efb-e1e6-4c9d-b60e-7535e5d6b7f3" width="500px">

* 공집합(빈트리), 노드가 1개인 트리 => 모두 Binary Tree(이진 트리)!!
  * `WHY?` 루트 노드를 중심으로 두 개의 서브 트리(큰 트리에 속하는 작은 트리)로 나뉘어 진다. 또한 나뉘어진 두 서브 트리도 모두 이진 트리어야 한다. 재귀적인 정의라 맞는듯 하면서도 이해가 쉽지 않을 듯하다. 한 가지 덧붙이자면 공집합도 이진 트리로 포함시켜야 한다. 그래야 재귀적으로 조건을 확인해갔을 때, leaf node에 다다랐을 때, 정의가 만족되기 때문이다. 자연스럽게 노드가 노드가 하나 분인 것도 이진 트리 정의에 만족하게 된다.
* Level(레벨) / height(높이)
  * 트리에서 각 `층별로` 숫자를 매겨서 이를 트리의 Level(레벨)이라고 한다. 레벨의 값은 0부터 시작하고 따라서 루트 노드의 레벨은 0이다. 그리고 트리의 최고 레벨을 가리켜 해당 트리의 height(높이)라고 한다.
* Perfect Binary Tree(포화 이진 트리), Complete Binary Tree(완전 이진 트리), Full Binary Tree (정 이진 트리)
  * `Perfect Binary Tree(포화 이진 트리)`: 모든 레벨이 꽉 찬 이진 트리를 의미
    <img src="https://github.com/user-attachments/assets/19d5fe74-054f-4f65-84df-65c276169dfd" width="500px">
  * `Complete Binary Tree(완전 이진 트리)`: 위에서 아래로, 왼쪽에서 오른쪽으로 순서대로 차곡차곡 채워진 이진 트리를 가리켜 완전 이진 트리라고 한다.
    <img src="https://github.com/user-attachments/assets/5d21ca87-c7e6-416c-9911-61712bbb4407" width="500px">
  * `Full Binary Tree (정 이진 트리)`: 모든 노드가 0개 혹은 2개의 자식 노드만을 갖는 이진 트리를 가리켜 정 이진 트리라고 한다.
    <img src="https://github.com/user-attachments/assets/31fcb821-a0aa-4c9a-ada7-19c479bb0d06" width="500px">
  * `Degenerate Binary Tree(변질 이진 트리)`
    <img src="https://github.com/user-attachments/assets/c4c4ad04-f0dc-404e-a971-e9d3146c6290" width="500px">
    * `Left Skewed Binary Tree`: 모든 부모 노드는 왼쪽 자녀 노드만 가지는 트리
    * `Right Skewed Binary Tree`: 모든 부모 노드는 오른쪽 자녀 노드만 가지는 트리
  * `Balanced Binary Tree(균형 이진 트리)` => 모든 노드를 다 확인해봐야함!
    * 참고로 연결된 자식이 없으면 서브트리의 높이는 `-1`로 간주
    <img src="https://github.com/user-attachments/assets/d22fd165-be4a-45f0-9a99-ba05e71e1c44" width="500px">
* 배열로 구성된 `Binary Tree`특징
  * 노드의 개수가 n개이고, root가 0이 아닌 1에서 시작할 때, i번째 노드에 대해서 parent(i) = i/2. left_child(i) = 2i, right_child(i) = 2i+1 의 index값을 갖는다.

### Binary Search Tree
* 줄여서 `BST`
* 효울적인 탐색을 위해서는 어떻게 찾을까만 고민해서는 안된다. 그보다는 효율적인 탐색을 위한 저장방법이 무엇일까를 고민해야 한다. 이진 탐색 트리는 이진 트리의 일종이다. 단 이진 탐색 트리에는 데이터를 저장하는 규칙이 있다. 그리고 그 규칙은 특정 데이터의 위치를 찾는데 사용할 수 있다.
  * `규칙1`: 이진 탐색 트리의 노드에 저장된 키는 유일하다.
  * `규칙2`: 부모의 키가 왼쪽 자식 노드의 키보다 크다.
  * `규칙3`: 부모의 키가 오른쪽 자식 노드의 키보다 작다.
  * `규칙4`: 왼쪽과 오른쪽 서브트리도 이진 탐색 트리이다.
* 이진 탐색 트리의 탐색 연산은 `O(logN)의 시간 복잡도`를 가진다. 사실 정확히 말하면 O(h)라고 표현하는 것이 맞다. 트리의 높이를 하나씩 더해갈수록 추가할 수 있는 노드의 수가 두 배씩 증가하기 때문이다. 하지만 이러한 이진 탐색 트리는 SkewedTree(편향 트리)가 될 수 있다. 저장 순서에 따라 계속 한 쪽으로만 노드가 추가되는 경우가 발생하기 때문이다. 이럴 경우 성능에 영향을 미치게 되며, 탐색의 Worst Case가 되고, 시간 복잡도는 O(n)이 된다.
* 배열보다 많은 메모리를 사용하며 데이터를 저장했지만 탐색에 필요한 시간 복잡도가 같게 되는 비효율적인 상황이 발생한다. 이를 해결하기 위해 `Rebalancing 기법`이 등장하였다. 균형을 잡기 위한 트리 구조의 재조정을 Rebalancing이라고 한다. 이 기법을 구현한 트리에는 여러 종류가 존재하는데 그 중에서 하나가 뒤에서 살펴볼 Red-Black Tree이다.

> :arrow_double_up:[Top](#1-data-structure)    :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#1-data-structure)    :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)
> - [이진탐색트리(binary search tree)를 설명합니다~ 기본 개념과 트리를 순회하는 여러 방법, 이진탐색트리의 삽입/삭제/검색이 어떻게 동작하는지 예를 통해 설명드려요 :)](https://www.youtube.com/watch?v=i57ZGhOVPcI)

### 그래프와 트리의 차이점
<img src="./images/graph-vs-tree.png" width="70%" height="70%">

> :arrow_double_up:[Top](#1-data-structure)    :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#1-data-structure)    :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)

### Binary Heap
* 우선순위 큐(Priority Queue)
  ![image](https://github.com/user-attachments/assets/d7ad16f0-de89-48bd-bbaa-28f212cb2386)
  * 우선순위 큐는 우선순위가 가장 높은 데이터를 가장 먼저 삭제하는 자료구조입니다.
  * 우선순위 큐는 데이터를 우선순위에 따라 처리하고 싶을 때 사용합니다.
    * ex. 물건 데이터를 자료구조에 넣었다가 가치가 높은 물건부터 꺼내서 확인해야 하는 경우
  * 우선순위 큐를 구현하는 방법 2가지
    * 1. 단순히 리스트 사용 => 삽입: O(1) / 삭제: O(N)
      2. `힙(heap)을 이용하여 구현` => 삽입: O(logN) / 삭제: O(logN)
  * 사용
    * 프로세스 스케줄링(process scheduling)
    * heap sort => 정렬 시, 힙에서 차례대로 꺼내면 알아서 정렬되니깐!!
* Heap
  * 힙은 `완전 이진 트리(마지막 레벨에서 왼쪽부터 꽉꽉 채운)` 자료구조의 일종입니다.
  * 힙에서는 항상 루트 노드(root node)를 제거합니다.
    * `최소 힙`: 루트 노드가 가장 작은 값을 가짐, 가장 작은 데이터가 우선적으로 제거됨
    * `최대 힙`: 루트 노드가 가장 큰 값을 가짐, 가장 큰 데이터가 우선적으로 제거됨
> :arrow_double_up:[Top](#1-data-structure)    :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#1-data-structure)    :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)
> - [힙(heap)이란](https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)
> - [자료구조: 우선순위 큐(Priority Queue)와 힙(Heap)](https://www.youtube.com/watch?v=AjFlp951nz0)
> - [우선순위 큐와 힙의 개념과 차이, 사용 사례를 설명합니다! 힙이 어떻게 동작하는지도 예를 통해 자세히 설명합니다!](https://www.youtube.com/watch?v=P-FTb1faxlo)

### Red-Black Tree

> :arrow_double_up:[Top](#1-data-structure)    :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#1-data-structure)    :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)
> - [01. Red-Black Tree 개요](https://github.com/namjunemy/TIL/blob/master/Algorithm/red_black_tree_01.md)
> - [02. Red-Black Tree insert fix-up](https://github.com/namjunemy/TIL/blob/master/Algorithm/red_black_tree_02.md)
> - [03. Red-Black Tree delete, fix-up](https://github.com/namjunemy/TIL/blob/master/Algorithm/red_black_tree_03.md)

### B+ Tree
* `B Tree` => `자녀 노드의 최대 개수를 입맛에 맞게 결정해서 쓸 수 있다!!!`
  * 만약에 단 2개가 아니라 3개를 저장하고 싶다면..?
    ![image](https://github.com/user-attachments/assets/a3a5499d-ee7b-4eaf-a35b-356008b51b20)
    1. 자녀 노드의 최대 개수를 늘리기 위해서, 부모 노드에 key를 하나 이상 저장한다.
    2. 부모 노드의 key들을 오름차순으로 정렬한다.
    3. 정렬된 순서에 따라 자녀 노드들의 key값의 범위가 결정된다.
  * 파라미터
    ![image](https://github.com/user-attachments/assets/36c7945d-e577-44dc-a252-9c3ef1f71eaa)
  * `B tree 데이터 삽입 예제` --> 유튭 영상 참고
  * 특징
    * 모든 leaf 노드들은 같은 레벨에 있다
    * => balanced tree이고, 검색 avg case/wort case 모두 시간 복잡도가 O(logN)이므로 조회할때 항상 일정한 성능을 낸다~ good!!
* `B- Tree`
* `B+ Tree`
> :arrow_double_up:[Top](#1-data-structure)    :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#1-data-structure)    :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)
> - [(1부) B tree의 개념과 특징, 데이터 삽입이 어떻게 동작하는지를 설명합니다! (DB 인덱스과 관련있는 자료 구조)](https://www.youtube.com/watch?v=bqkcoSm_rCs)
> - [(2부) B tree 데이터 삭제 동작 방식을 설명합니다 (DB 인덱스과 관련있는 자료 구조)](https://www.youtube.com/watch?v=H_u28u0usjA)

---

## Reference
> - []()


## :house: [Home](https://github.com/WeareSoft/tech-interview)
