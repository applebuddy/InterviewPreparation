****

# 면접 질문 정리 

- 면접에 나올 수 있는 기초 질문에 대한 답변 정리
- by applebuddy



<br><br>

# @ 공통 질문



### # 자기소개

저는 민경태입니다. 인천대학교 컴퓨터공학과를 졸업했으며 이후 통신장교로 3년 복무했습니다. 전역 후 18년 말부터 iOS개발 분야에 입문하여 지금까지 개발자의 꿈을 이루기 위해 노력하고 있습니다. 제 가장 큰 장점은 설정한 목표를 끈기있게 도전하고 달성하는 실행력입니다. 항상 제 자신을 위한 미션을 만들고 끊임없이 이루고 발전하기 위해 노력하고 있습니다. 

제 꿈은 전문성을 바탕으로 열정과 지식을 많은 사람들에게 나눌 수 있는 개발자입니다. 제 꿈을 이루기 위해 부스트코스 iOS과정을 수료했으며 이후 개발자 오픈채팅방 운영 및 커뮤니티 참여를 통해 열정적인 개발자들과 소통하며 트랜드에 뒤쳐지지 않으려 노력하고 있습니다. 현재는 IT동아리인 프로그라피에서 iOS개발을 맡아 협업프로젝트를 진행하고 있습니다. 인턴지원을 계기로 뛰어난 개발자 분들과 열정적으로 일하며 성장할 수 있는 기회를 만들고 싶습니다. 감사합니다.

<br><br>

### # 마지막으로 하고싶은 말

.



<br><br>

### # 성취 해본 가장 인상적인 경험





<br><br>

# @ CS 기술 질문



## # 알고리즘

## ## 자료구조

### **연결리스트 (Linked List)**

- **선형적으로 단방향으로 연결된 값의 컬렉션**
- **각각의 노드는 값과 next 포인터를 갖고 있다.** 
- **Head Node 추가 시 제외한 일반적인 추가, 삭제 등의 시간복잡도는 O(N)으로 비효율** 적인 편인 자료구조
- **연결리스트, Linked List 구현 예시 ▼**

~~~ swift

// MARK: Implementation of LinkedList in Swift
// MARK: - Node Definition
public class Node<T> {
    public var value: Int
    public var next: Node?
    
    public init (value: Int, _ next: Node? = nil) {
        // 두번째 매개변수는 만약 지정되지 않았을 때 default값을 nil로 주도록 설정한다.
        self.value = value
        self.next = next
    }
}

// MARK: - Prints Node Data
extension Node: CustomStringConvertible {
    public var description: String {
        guard let next = next else {
            return "\(value)" // 다음 노드가 없다면 현재 값만 출력한다.
        }
        
        // 다음 노드(next)가 존재한다면 guard let 이후 코드도 실행된다. -> 다음 노드도 출력한다.
        return "\(value) -> \(String(describing: next)) "
    }
}

let node1 = Node<Int>(value: 1)
let node2 = Node<Int>(value: 3)
let node3 = Node<Int>(value: 5)
node1.next = node2
node2.next = node3
print(node1.description)

~~~

<br><br>

### **이진트리, Binary Tree**

- **각각 0~2개의 노드를 갖는 이진트리 자료구조**
- **각 노드는 leftChild?, rightChild?, 자신의 value를 갖는다.** 
- **모든 노드가  leftChild, rightChild를 갖는 트리를 Full Tree** 라고 한다. 
- **Full Tree 상태 + 최하위 노드가 몇개 비어있는 경우에는 작은 의미로  Complete Binary Tree**라고 하며, Heap 자료구조로서 활용될 수 있다.
- **InOrder** 
  - **트리를 최 좌측 부터 우측 순으로 차례대로 출력**하는 순서 방식 
  - **중간에 RootNode의 순서**가 온다. 
  - **처음에 RootNode의 leftChild를 순회하는 재귀호출 -> rootNode 값을 출력 -> rightChild를 순회하는 재귀호출**
- **PreOrder**
  - **처음에 RootNode의 순서**가 온다.
  - **처음에 RootNode 값을 출력 -> leftChild를 순회하며 출력하는 재귀 호출 -> rightChild를 순회하며 출력하는 재귀 호출**
- **PostOrder**
  - **마지막에  RootNode의 순서**가 온다.
  - **처음에 leftChild를 순회하며 출력하는 재귀호출 -> rightChild를 순회하며 출력하는 재귀호출 -> 마지막에 RootNode 값을 출력**
- **이진트리, Binary Tree 구현 예시 ▼**

~~~ swift
// MARK: - 이진트리, Binary Tree Example

public class BinaryTreeNode<T> {
    public var value: T
    public var leftChild: BinaryTreeNode? // 왼쪽 자식노드
    public var rightChild: BinaryTreeNode? // 오른쪽 자식노드
    public init(value: T) {
        self.value = value
    }
    
    // In-Order 탐색
    public func traverseInOrder(visit: (T) -> ()) {
        leftChild?.traverseInOrder(visit: visit)
        visit(value) // 값을 받아 실행하는 반환값 없는 클로저가 실행되는데 이때의 값은 순회중인 현재 인스턴스의 value가 된다.
        rightChild?.traverseInOrder(visit: visit)
    }
    
    public func traversePreOrder(visit: (T) -> ()) {
        visit(value)
        leftChild?.traversePreOrder(visit: visit)
        rightChild?.traversePreOrder(visit: visit)
    }
    
    public func traversePostOrder(visit: (T) -> ()) {
        leftChild?.traversePostOrder(visit: visit)
        rightChild?.traversePostOrder(visit: visit)
        visit(value)
    }
}

let rootTree = BinaryTreeNode<Int>(value: 0)
let one = BinaryTreeNode<Int>(value: 1)
let two = BinaryTreeNode<Int>(value: 2)
let three = BinaryTreeNode<Int>(value: 3)
let four = BinaryTreeNode<Int>(value: 4)
let five = BinaryTreeNode<Int>(value: 5)

rootTree.leftChild = one
rootTree.rightChild = two
one.leftChild = three
one.rightChild = four
two.leftChild = five

// traverseInOrder의 처음이자 마지막 매개변수는 값을 받아 실행하는 클로져였다.
// 마지막 매개변수이므로 해당 클로져는 후행클로져 형태로 넣어 아래와 같이 실행할 수 있다.
// 현재 구성한 트리의 상태 ▼

//.        0 <- Root Node
//.    1       2  <- Sub Node
//.  3   4   5

// InOrder 출력 결과 -> 3 1 4 0 5 2
print("traverseInOrder Result ▼")
rootTree.traverseInOrder { print($0, terminator: "->") }
print()
print("traversePreOrder Result ▼")
rootTree.traversePreOrder { print($0, terminator: "->") }
print()
print("traversePostOrder Result ▼")
rootTree.traversePostOrder { print($0, terminator: "->") }

// traverseInOrder Result ▼
// 3->1->4->0->5->2->
// traversePreOrder Result ▼
// 0->1->3->4->2->5->
// traversePostOrder Result ▼
// 3->4->1->5->2->0->
~~~

<br><br>

### ## Sorting Methods, 정렬 방법

- **안정정렬/불안정정렬의 차이** : **같은 값이 존재할때 해당 값들의 인덱스 순서가 정렬 후에 유지될 수 있는지 여부에 따라 결정**된다. 

- **퀵 정렬 (Quick Sort)**
  - **평균적으로 단일 정렬기법 중 가장 좋은 성능을 보이는 정렬방법**, **비펏을 기준으로 피벗보다 작은값, 큰값을 양옆으로 비교하며 재귀, 분할정복방식으로 정렬을 수행**한다. 
  - **파티션, 분할정복을 활용**한다. 
  - 같은 값의 인덱스 위치가 바뀔 수 있는 불안정 정렬
  - **최적의 상황에서 복잡도는 O(NlogN)** 이다.
    - 분발정복 알고리즘이 적용되어 정렬 체크구간이 쪼개질 수록 복잡도가 줄어든다.
  - **최악의 상황에서 복잡도는 O(N^2)** 이다.
    - **이미 정렬이 되어있는 상태에서 비펏이 양 끝에 위치할 경우 N^2번을 순회**하며 분할정복의 이점을 활용하지 못하기 때문이다. 
  
  ~~~ swift
  // MARK: - QuickSort Example with Swift
  import Foundation
  
  func quickSort(_ arr: inout [Int], _ start: Int, _ end: Int) {
      if start >= end { return } // 원소가 한 개인 경우 바로 종료
      
      let key = start // 키는 첫번째 원소
      var i = start + 1
      var j = end
      var temp = 0
      
      while i <= j { // 엇갈릴 때 까지 반복
          while arr[i] <= arr[key] {
              i += 1
          }
          
          while arr[j] >= arr[key] && j > start {
              j -= 1;
          }
          
          if i > j {
              temp = arr[j]
              arr[j] = arr[key]
              arr[key] = temp
          } else {
              temp = arr[i]
              arr[i] = arr[j]
              arr[j] = temp
          }
      }
      
      quickSort(&arr, start, j-1)
      quickSort(&arr, j+1, end)
  }
  
  var arr = [3,1,5,4,2,6,9,7,8,0]
  quickSort(&arr, 0, arr.count-1) // 퀵정렬에 의해 오름차순 정렬이 된다.
  print(arr) // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
  
  ~~~

<br>

- **병합 정렬 (Merge Sort)**
  - 퀵정렬과 함께 분할정복 정렬 알고리즘 기법 중 하나
  - 안정 정렬
- **게수정렬(Counting Sort)**
  - 계수가능 범위에서 배열 인덱스를 이용해 요소를 정렬한다. 
  - **복잡도는 O(N)로 매우 효율적**이다.
  - **일정 이상의 계수범위를 넘어갈 시 메모리의 과부하가 발생**할 수 있다. 
    - 매우 큰 계수 범위에 대한 사용 제한
- **힙 정렬 (Heap Sort)** 
  - Complete Binary Tree를 이용한 Heap 정렬
  - 불안정 정렬
  - **일반 적인 복잡도는 O(NlogN)이다.**
- **삽입 정렬 (Insert Sort)**
  - 인간이 기본적으로 정렬할때 사용하는 방법과 유사한 기법
  - **일반 적인 복잡도는 O(N^2)이다.**
  - 하지만 **배열의 사이즈가 적거나 이미 정렬이 거의 되어 있는 경우 빠른 속도**를 보여주며 이로인해 **팀 정렬, 인트로 정렬 등의 하이브리드 정렬기법에 함께 활용**되기도 한다. 
- **팀 정렬 (Tim Sort)**
  - **자바, 파이썬, 스위프트 등의 언어에서 기본 정렬로 제공하는 하이브리드 정렬 기법**
  - **병합 + 삽입정렬의 하이브리드 정렬**기법
- **인트로 정렬 (Intro Sort)**
  - **C++ 등의 언어에서 기본 정렬로 제공하는 하이브리드 정렬 기법**
  - **퀵 + 힙정렬 + (삽입정렬)의 하이브리드 정렬**기법
    - 팀 정렬처럼 정렬 파티션이 적을때 삽입정렬을 혼용하기도 한다. 

<br>

## ## C++ 문법 용어 정리

- **C++ 언어의 특징**
  - **대표적인 객체지향 프로그래밍 언어** 
    - **캡슐화**
      - 캡슐화된 객체의 세부 내용은 외부에서 볼수 없게 숨길 수 있다. 
      - **정보 은닉 및 재사용의 용이성**
    - **추상화**
      - **객체의 속성 중 가장 중요한 것에 중점을 두어 모델링** 하는 것
      - **프로그램 구조 및 구성을 직관적으로 볼 수 있다.** 
    - **상속성**
      - **상위 클래스의 속성을 물려받은 자식 객체를 정의할 수 있다.** 
      - **소프트웨어 재사용성을 증대**시켜준다. 
    - **다형성**
      - **오버라이딩을 지원하여 virtual 키워드 등을 통해 오버라이딩 된 자식클래스의 메서드나 프로퍼티를 사용할 수 있다.** 
      - **다형성을 통해 같은 이름의 메서드여도 어떤 객체를 접근하냐에 따라 고유한 방법으로 사용가능**하다.
  - **C++은 정적바인딩을 원칙**으로 작동한다.
    - **동적바인딩을 통해 서브클래스의 오버라이딩 메서드를 사용하기 위해서는 virtual등의 키워드 지정이 필요**하다.

<br>

- **배열 포인터 vs 포인터 배열**
  - **배열 포인터는 배열의 시작주소값을 저장하는 포인터**이다.
  - **포인터 배열은 주소값들을 저장하는 배열**이다.

<br><br>

## # 네트워크

### ## HTTP 

- **하이퍼텍스트 전송 프로토콜** (Hyper Text Transfer Protocol)
- **클라이언트 ~ 서버 간 이루어지는 요청(Request)/응답(Response) 프로토콜**



### ## HTTP 응답코드 종류

- 100
  - Continue, 클라이언트로부터 일부 요청을 받았으며 나머지 정보를 계속 요청
- **2xx**
  - 일반적으로 **요청이 성공적으로 수행 될 경우 2xx 응답코드를 수신**한다. 
- 3xx
  - 리다이렉션 -
- **4xx**
  - **클라이언트 측 오류** 응답 코드
- **5xx**
  - **서버 측 오류** 응답 코드

<br>

### ## HTTP 메서드 종류

- **GET**
  - GET 요청 방식은 **서버 특정 URL이 가진 정보를 읽기위해 요청하는 메서드**이다.
- **POST**
  - POST 요청 방식은 **서버 특정 URL에 데이터를 전송해서 추가할 때 사용**한다. 
  - 클라이언트 측에서 명확한 자원의 위치를 지정하지 않는다. 

- HEAD
  - GET 요청방식과 유사하나 단, **헤더정보만 가져온다.** 
- OPTIONS
  - 웹서버에서 지원되는 메소드 종류를 확인한다.
- PUT
  - **자원을 전체적으로 업데이트 요청** 한다. 
  - 클라이언트 측에서 명확한 자원의 위치를 지정한다. 
- PATCH
  - **자원 일부를 업데이트 요청** 한다. 
- DELETE
  - **특정 자원을 삭제 요청**한다.



### ## OSI 7계층

- 1) 물리 계층
- 2) 데이터링크 계층
- 3) 네트워크 계층
- 4) 전송 계층
- 5) 세션 계층
- 6) 프레젠테이션 계층
- 7) 애플리케이션 계층

### ## TCP/IP 4계층

- 1) 네트워크 접근 계층
- 2) 인터넷 계층
- 3) 전송 계층
- 4) 애플리케이션 계층



### ## TCP vs UDP

- TCP (Transmission Control Protocol)
  - 전송 제어 프로토콜 규약
  - 연결형 서비스로 가상 회선 방식을 제공
  - 3-way handshaking 과정을 통해 연결설정, 4-way handshaking으로 해제한다. 
    - 목적지 ~ 수신지를 확실히 하여 정확한 전송 보장을 위해 3-way/4-way handshaking을 사용한다. 
  - 높은 신뢰성을 보장한다. 
  - UDP보다 느리다.
  - 전이중(Full-Duplex), 점대점(Point to Point) 방식
- UDP (User Datagram Protocol)
  - 사용자 데이터그램 프로토콜 규약
    - 데이터를 데이터그램 단위로 처리하는 규약
    - 데이터그램 : 독립적인 관계를 지니는 패킷
  - 비연결형 서비스
  - 서버 소켓은 연결만을 담당한다. 
  - 서버 ~ 클라이언트는 1대1로 연결된다. 
  - 전송 데이터의 크기가 무제한인다.
  - 신뢰성을 보장할 수 없다. 
  - TCP보다 빠르다.

<br><br>



## # 데이터베이스



### ## DBMS

- 데이터베이스 관리 시스템 (Database Management System)
  - 다수의 사용자들이 DB 내의 데이터를 접근할 수 있도록 해주는 SW도구의 집합



### ## 데이터베이스 문법

- **SELECT** [열]

  - **특정 열을 선택하는데 사용**한다. **(필수)**

- **FROM** [테이블]

  - **특정 테이블을 조회할 때 사용**한다. **(필수)**
  - **"A" 테이블의 전체열 조회 예시 ▼**

  ~~~ sql
  SELECT * FROM "A" 
  ~~~

  

- **WHERE** [조건]
  
- 특정 조건에 따라 조회할 때 사용한다. (선택)
  
- **GROUP BY**

  - **동일한 값을 가진 데이터를 집계해서 조회하고자 할 때 사용**하는 문장 (선택)

- **ORDER BY**

  - **오름차순(ascribing) or 내림차순(describing)으로 정렬할때 사용**하는 문법

  ~~~ sql
  SELECT NAME, COUNT(NAME) FROM TABLE
  FROM CART_PRODUCTS GROUP BY CART_ID ORDER BY COUNT(NAME);
  ~~~

  

<br>

### ## 데이터베이스 용어정리

- **NoSQL**
  - Not Only SQL의 약자, 기존의 RDBMS와 다른 형태의 데이터로 저장하는 기술
  - 트랜잭션을 지원하지 않는다.

- **트랜젝션**
  - 데이터베이스 내에서 한꺼번에 수행되어야 할 일련의 연산집합
  - **트랜잭션은 데이터베이스의 논리적 연산단위**이다.
- **DDL** (Data Definition Language)
  - 데이터 정의 언어
  - 데이터베이스 스키마를 정의 or 조작하기 위해 사용한다. 
  - CREATE, ALTER, DROP, TRUNCATE 등이 있다. 
- **DML** (Data Manipulation Language)
  - 데이터 조작 언어, 데이터를 조작하기 위해 사용한다. 
  - SELECT, INSERT, DELETE, UPDATE
- **DCL** (Data Control Language)
  - 데이터 제어언어
  - 데이터의 보안, 무결성 등을 정의하는데 사용한다. 
  - COMMIT, ROLLBACK, GRANT, REVOKE
- **DQL** (Data Query Language)
  - SELECT만을 따로 분리해서 쿼리로 표현하는 언어
- **TCL** (transaction Control Language)
  - 트랜젝션 제어 언어

<br><br>



# @ Swift 기술 질문

### # 애플리케이션 Life Cycle

- **iOS Application's Life Cycle** (SceneDelegate 추가 전 기준)
  - UIApplication 객체생성  -> @UIApplicationMain 어노테이션 식별 후 AppDelegate 싱글톤 객체 생성 -> 이후 Main Event Loop를 실행 + AppDelegate의 상황에 따른 감지 및 작업처리
  - Not Running
  - Foreground
    - Inactive
    - Active
  - Background
  - Suspended

- AppDelegate Delegate Methods
  - application(_: didFinishLaunchingWithOptionsa:) 
    - 앱이 처음 시작될 호출되는 델리게이트 메서드
  - applicationDidBecomeActive(_ application: UIApplication)
    - Foreground의 Active 상태가 될때 호출되는 델리게이트 메서드
  - applicationWillResignActive(_ application: UIApplication) 
    - Foreground의 Inactive상태가 될 때 호출되는 델리게이트 메서드
  - applicationDidEnterBackground(_ application: UIApplication) 
    - Foreground -> Background 진입 시 호출되는 델리게이트 메서드
  - applicationWillenterForeground(_ application: UIApplication)
    - Background -> Foreground 진입 예정 시 호출되는 델리게이트 메서드
  - applicationWillTerminate(_ application: UIApplication)
    - Application 종료 직전 호출되는 델리게이트 메서드



<br><br>



### # 뷰 컨트롤러의 Life Cycle

- ViewController의 라이프 사이클 순서 
  - init -> loadView -> viewDidLoad -> viewWillAppear -> viewDidAppear ->viewWillDisappear -> viewDidDisappear -> viewDidUnload(Deprecated)

<br><br>

#### 1) init() 

- 스토리보드[init?(coder:)]나 nib(xib)[init(nibName:bindle:)]파일을 통해 뷰 컨트롤러를 초기화하고뷰를 만들때 사용할 정보를 뷰컨트롤러에 전달하는 단계입니다. 

#### 2) LoadView()

- **뷰를 실제로 생성 후 메모리에 로드**합니다. 만약 **스토리보드나 nib(xib)를 사용하지 않는다면 해당 메소드를 오버라이드에서 뷰를 생성, 뷰계층을 구성**해야합니다. 

#### 3) viewDidLoad()

- loadView()로 뷰가 메모리에 로드된 직후에 해당 메소드를 호출합니다. 이때 뷰 or 뷰컨트롤러에 대한 추가적인 설정을 합니다. 

#### 4) viewWillAppear(_:)

- view가 view계층에 추가되기 직전, 뷰 애니메이션이 설정되기 전에 호출된다. 뷰가 화면에 나타나기 전에 해당 viewWillAppear를 오버라이드해서 필요한 작업을 수행할 수 있다. viewWillAppear를 오버라이드 하기 전에는 반드시 부모클래스의 viewWillAppear를 호출하도록 정의해야 한다. 
  - ☆ 만약 어떤 뷰컨트롤러가 다른 뷰컨트롤러를 popover 방식으로 띄운 후, 해당 뷰컨트롤러가 사라질때는 예외적으로 popover를 실행한 뷰 컨트롤러의 viewDidAppear가 실행되지 않는다. 

#### 5) viewDidAppear(_:)

- view가 view계층에 추가된 직후에 실행됩니다. 해당 메서드를 오버라이드 해서 나타나는 뷰에 대한 추가적인 설정을 할 수 있는데 이때 반드시 부모 클래스의 viewDidAppear를 호출하도록 정의해야 합니다. 

#### 6) viewWillDisappear(_:)

- view가 view계층에서 제거되기 직전에 viewWillDisappear(_:)가 호출됩니다. view가 view계층에서 제거되기 직전 최초 반응가(first responder)상태를 내려놓거나, 뷰의 설정 등의 작업이 가능합니다. viewWillDisappear를 오버라이드할때는 반드시 부모 클래스의 viewWillDisappear를 호출해야 합니다. 

#### 7) viewDidDisappear(_:) 

- view가 view계층에서 제거된 이후에 호출됩니다. viewDidAppear(_:)에서 뷰가 제거된 후의 작업을 할 수 있으며 이때 부모클래스의 viewDidDisapear를 호출해야 합니다. 

#### - didReceiveMemoryWarning()

- 앱 실행 간 시스템 메모리가 부족한 상황이 되면, 시스템은 뷰컨트롤에 메모리가 모자라다는 메세지를 보내며 didReceiveMemoryWarning()메서드를 호출합니다. 
- iOS6 이전 메모리 부족에 따라 시스템이 임의적으로 뷰를 헤제하던 것에서 iOS6 이후에는 시스템이 직접 관여하지 않게 되므로서 임의 해제에 사용하던 viewWillUnload / viewDidUnload는 deprecated되었습니다.
  - 그걸 didReceiveMemoryWarning에서 처리하게 됨

뷰 컨트롤의 참조가 0이 되면 deinit()을 통해 뷰컨트롤러가 가지고 있던 뷰와 관련 자원들을 해제함으로서 완련히 ViewController의 생명주기가 끝나게 됩니다...



<br><br>



### # iOS 주요 클래스, Main Classes 

### NSObject

- Objective-C 클래스 계층 구조의 Root Class

~~~ swift
class NSObject
~~~



<br><br>

### # 라이브러리, Library

- 프로그램이 연결할 수 있는 패키징 된 객체 파일들의 모음
- 라이브러리 종류
  - 정적라이브러리
  - 공유라이브러리



<br><br>



### # 프레임워크, FrameWorks

- 라이브러리는 실행가능한 코드일 뿐이지만 프레임쿼크는 다른 리소스의 하위 디렉토리를 포함하는 번들이다. 

#### ## 코코아 터치 프레임워크 

- **코코아 터치 프레임워크 (Cocoa Touch FrameWork) 는 iOS 애플리케이션 개발환경**이다.
- **macOS 애플리케이션 제작 & 기능구현에 필요한 프레임워크를 포함하는 최상위 레벨의 프레임워크**이다. 
- **코코아 터치는 핵심 프레임워크인 UIKit, Foundation을 포함**한다. 
- **코코아 (Cocoa) 란 NSObject를 상속받는 모든 클래스 및 객체를 가리킬 때 사용하는 단어**이다. 
- 코코아 (Cocoa) 란 이름의 기원
  - **커피원산지에서 따온 Java언어에 대항해 어린아이도 할 수 있는 Java라는 의미로 코코아 Cocoa로 명명**했다. 

#### ## Foundation FrameWork

- **CocoaTouch FrameWork에 포함되어있는 프로그램의 중심을 담당하는 프레임워크**이다. 
- **기본적인 원시 데이터 타입 (String, Int, Double) 등이 Foundation에 포함**되어있다. 
- **Foundation 기본 기능 셋**
  - Number, Data, String
    - **원시 데이터 타입의 사용**
  - Collection 
    - **Array, Dictionary, Set 등의 컬렉션 타입 사용**
  - Date, Time
    - **날짜와 시간을 계산하거나 비교**
  - Unit, Measurement
    - 물리적 차원을 숫자로 표현, 관련 단위 간 변환 가능
  - Data Formatting
    - **숫자, 날짜, 측정값 등을 문자열로 서로 변환**하는 작업
  - Filter, Sorting 
    - **컬렉션의 요소를 검사, 정렬**하는 작업



#### ## UIKit FrameWork

- **CocoaTouch FrameWork에 포함되어있는 iOS 애플리케이션의 사용자 인터페이스를 구현하고 이베느를 관리하는 프레임워크**이다.

- **UIKit 기본 기능 셋**

  - **Gesture 처리, Animation, 그림그리기, 이미지/텍스트 처리 등 사용자 이벤트 처리를 위한 클래스를 제공**
  - **애플리케이션의 화면을 구성하는 요소를 제공**
    - **UIxxx 뷰요소들을 포함, UITableView, UICollectionView, UITextField, UILabel, UIAlertController** 등...

  - ✭ **UIKit 클래스 중 UIResponder에서 파생 된 클래스나 사용자 인터페이스 관련(UI) 클래스들은 애플리케이션의 메인스레드에서만 사용해야한다.** 
    - **User Interface와 관련 된 UI 관련 이벤트는 Main Thread에 붙어있기 때문에 메인스레드에서먄 UI를 처리해야한다.**

<br><br>

### # 접근제한자

- **open**
  - **완전 개방상태의 접근제한자**
  - **현재 모듈, 다른 모듈 모두 읽기, 할당, 상속, 오버라이딩이 가능**하다. 

- **public** 

  - **현재 모듈, 다른 모듈 모두 읽기가 가능**하다.
  - **다른 모듈에서는 할당, 서브클래싱, 상속, 오버라이딩이 불가능**하다. 

- **internal**

  - **별도의 접근제한자르 지정 안할 시 지정되는 default 접근제한자**
  - **현재 모듈 내에서만 읽기, 할당, 상속, 오버라이딩이 가능**하다.

- **fileprivate**

  - **지정한 file 내에서만 읽기, 할당, 상속, 오버라이딩이 가능**하다.

- **private(set)**

  - **지정한 블럭 내에서만 읽기, 할당, 상속, 오버라이딩이 가능**하다.
  - **블럭 외부에서는 읽기만 가능**하다.

- **private**

  - **지정한 블럭 내에서만 읽기, 할당, 상속, 오버라이딩이 가능**하다.

  - **블럭 외부에서는 private 멤버를 알 수 없다.**

<br><br>

### # 프로퍼티의 종류

### ## 저장 프로퍼티 

- **기본적인 형태의 프로퍼티 선언** 
- 말 그대로 특정 값을 저장해 놓은 프로퍼티

~~~ swift
var numb: Int = 0 // 저장 프로퍼티
~~~

<br>

### ## 계산 프로퍼티 

- **읽기, 쓰기에 따른 값을 그때그때 계산한 값을 내놓는 프로퍼티**
- **get or get+set 으로 구성**된다.
  - **get 만 구현할 경우 return ~~~ 으로만 표현**해도 된다. 

~~~ swift
class Point {
  	var pValue: Int = 0
  
  	// 읽기(get)만 지원하는 계산프로퍼티, calcValue
  	var calcValue: Int { 
        return pValue
    }
  
  	// getter, setter를 모두 지원하는 계산프로퍼티, calcValue2
    var calcValue: Int {
      	get {
          	return pValue * 2 // 반환은 상수만 반환하거나 별도의 저장프로퍼티를 활용한 값을 반환할 수 있다. 
        }
      	set {
          	pValue = newValue * 3
        }
    }
}
~~~

<br>

### ## 프로퍼티 감시자 

- **값이 변화했을때 변화전 or 변화후의 값을 처리할 수 있는 프로퍼티**
- **didSet(값 변동 시 이전 값(oldValue)을 통해 처리) or willSet(값 변동 시 변동된 값(newValue)을 통해 처리)을 사용**한다. 
- **계산 프로퍼티 기능과 함께 사용할 수 없다.** 

~~~ swift
// 프로퍼티 감시자 (Observer Property) 사용 예시
private var isAPIDataRequested: Bool = false {
  	willSet {
      	DispatchQueue.main.async {
          	// 값이 바뀌었을 때 바뀐 값이 true면 데이터 로딩을 실행, 반대의 경우 데이터 로딩을 중단한다. 
          	if newValue {
								self.startDataLoading()
            } else {
              	self.stopDataLoading()
            }
        }
    }
}
~~~

<br>

### ## Lazy 프로퍼티

- **Lazy 변수는** 초기화 후 **실제 사용되었을때 부터 연산**이 된다. 
- **Struct, Class에서만 Lazy 사용이 가능**하다. 
- **Lazy 변수는 var와 사용가능하며 lazy let은 사용 불가능**하다. 
  - **실제 사용 이후에 연산이 되지만 이전에 이미 초기화를 한 뒤 접근하는 것이기 때문에 lazy var 의 형식으로 사용**한다. 
- **Lazy 변수를 실제 처음 사용할 때 연산할 값을 넣어주기 위해 초기화 시 Closure ' {...}() ' 를 넣어준다.**

~~~ swift
class Person {
  	var name: String
  	// 클로저 내에서 self.를 참조하여 순환참조가 발생할 여지가 있으므로 [weak self] 키워드를 지정한다. 
  	lazy var greeting: () -> String = { [weak self] in 
    		return "Hello my name is \((self?.name)!)"                                  
    }
}

var me = Person(name: "applebuddy")
print(me.greeting()) // Hello my name is applebuddy
me.name = "Mingoony"
print(me.greeting()) // Hello my name is Mingoony
~~~

<br>

- **당장 사용할 가능성이 적은 컨텐츠를 메모리로 쌓아두면 쓸데없이 메모리만 차지하고, 애플리케이션 실행 시 부하**가 올 수도 있다. 
  - **바로 사용하지 않을 수 있는 비교적 메모리 소요가 큰 멤버에 대해 lazy 키워드를 추가하여 메모리 효용성을 높힐 수 있다.** 



<br><br>

### # ARC 란 무엇인가요?

- ARC는 Automactic Reference Counting의 약어이다.
- ARC는 컴파일 시점에 동작하며 코드를 빌드(컴파일) 할 때 객체의 RC(Reference Count)를 추척하여 0이 되는 시점에는 자동으로 release 코드를 넣어 해제해주는 방식을 말한다. 

<br><br>





### # 옵셔널이란 무엇인가요?

- 강타입 언어인 Swift는 타입 안정성을 중요시한다. 그런 Swift언어에서 값이 없을 수(nil) 있음을 표현하는 것이 옵셔널이다. 
- 옵셔널은 모나드의 일종이다. 
- 옵셔널 변수는 끝에 ''?'' 키워드가 붙으며 이는 강제언래핑(!) or 옵셔널바인딩을 통해 옵셔널을 실제 있는 값으로 래핑하여 사용할 수 있다. 

<br><br>



### # map, flatMap, compactMap의 차이점

- Map 
  - **Sequence 요소들을 지정한 작업으로 Mapping** 시킨다. -> 결과에 Optional 중첩이 생길 수 있다.  
- FlatMap
  - **filter { $0 != nil } + 시퀀스들을 합쳐서 반환**한다.
  - map + flatten의 속성이 더해진 함수
  - Non-nil 상태(Optional값이 아닌) 결과들을 갖는 배열을 리턴한다. 
- CompactMap 
  - **fillter { $0 != nil } + mapping 후 결과를 반환**한다.
  - 1차원 배열 시퀀스에 대한 반환 결과는 FlatMap과 CompactMap이 동일하다. 



<br><br>

### # MVC 패턴

- **Model - View - Controller로 구성된 모델-뷰-컨트롤러 디자인패턴 기법**
- **M/V/C 각자 역할** 
  - **Model**
    - **View와는 절대 소통하지 못한다.** 
    - **사용자에게 보여주기 위한 Controller에 필요한 데이터를 제공**한다.
      - **KVO/NotificationCenter,Singleton,constant struct 등을 통해 컨트롤러와 블라인드 소통**한다. 
  - **View**
    - **Model과는 절대 소통하지 못한다.** 
    - **Controller와는 블라인드 상태로 소통**해야한다. 
      - View는 Controller가 어떤목적의 Controller인지 알 수 없다.
    - **Controllers에 제공되는 브라인드 소통 방법**
      - **타겟 메서드** : **Controller에서** **@IBOutlet(아울렛), @IBAction(타겟메서드)등의 형태로 사용가능**하다.
      - **델리게이트** : **Controller에서** **View요소의 delegate, dataSource 등을 self로 할당하여 사용가능**하다. 
        - **View의 delegate변수에 weak 지정을 해주어 Controller self 참조의 의한 순환참조를 방지**할 수 있다. 
  - **Controller**
    - **Model로부터 KVO/NotificationCenter,Singleton 방법 등으로 상황에 따른 데이터를 받고 사용**한다. 
    - **필요한 View에 대한 @IBOutlet, @IBAction, Delegation Pattern 등을 활용하여 블라인드로 소통**하며 사용할 수 있다. 

- **MVC의 장점**
  - **iOS 환경에서 기본적으로 제공하는 디자인패턴 기법**으로 **초보자도 이해하기 쉽고 빠르게 구현**하기 쉽다.
  - **가벼운 프로젝트를 만드는데 유리**하다. 
- **MVC의 단점**
  - **Massive ViewController** 
    - **비대해지는 뷰 컨트롤러**의 문제점
    - **iOS에서 ViewController의 비중이 크고** 상대적으로 **ViewController만 유독 거대해질 가능성**이 있다.
  - **Testability**
    - 앞서 말했던 **Massive ViewController의 성질로 인해 Test하는데 있어 불편함**이 생길 수 있다. 
    - 상대적으로 비대해지는 ViewController에 대한 유지보수의 문제점

<br><br>

### # 순환참조란 무엇인가요?

- 데드락(DeadLock), 교착상태, 병목현상이라고도 한다. 
- 힙에 참조된 객체가 서로가 헤제되기를 무한정으로 기다리며 병목현상이 일어나는 것을 말함

#### - Closure Capturing

- iOS개발 간 마주할 수 있는 대표적인 예시로는 Closure Capturing이 있음.

~~~ swift 
class Zerg {
  // [weak self] or [unowned self]등을 사용하지 않으면...
  // Zerg객체는 foo를 참조
  // foo는 Zerg객체의 멤버를 참조함으로서 ClosureCapturing 문제를 일으킬 수 있다.
  private var foo = { [weak self] in 
  	// [weak self]를 설정 시 클로져 캡쳐링 문제를 해결 할 수 있다. 
 		// weak는 Optional이기 때문에 옵셔널 체이닝을 통해 접근한다. 
		self?.bar()
	}
  private func bar() { ... }
}
~~~



#### 객체 간 순환참조를 발견하는 방법과 해결방법

- Instrument의 Leak 도구를 이용해서 체크
- deinit을 활용하여 로깅코드를 통해 체크한다. 
- Xcode Memory Graph를 이용해서 Live Object를 확인, Leaking Object 확인



<br><br>



### # strong, weak, unowned 키워드의 의미와 차이는 무엇인가요?

- Strong 

  - 기본적으로 default는 strong으로 지정된다. 

  - strong 키워드로 선언된 멤버는 할당되는 순간 AC(Reference Count)를 증가시키고 1로 시작한다. 

  - RC를 증가시켜 ARC 사용 간 메모리 해제를 피하고 객체를 안전하게 사용하고자 할 때 사용한다. 

  - 예를 들어 A라는 메서드에 a라는 레퍼런스 객체를 생성 (1 + 1 == 2) -> A 메서드 내에서 사용하고 A메서드가 종료하더라도 (2 - 1 == 1) RC는 0이 되지 않아 이후 다른 곳에서도 해제되지않고 해당 객체의 사용이 가능해진다. 

    - 다만 Closure 내에서 strong self 멤버를 사용 시, Closure Capturing 등의 문제 상황이 발생할 수 있어 주의가 필요하다. 

  - strong 객체 A 사용 예시 ▼

    ~~~ swift
    
    class A: CustomStringConvertible {
      var description: String {
        return "Class A"
      }
    }
    
    func someMethod() {
      let a = A() // a Reference Count 0+1 == 1
      DispatchQueue.main.async {
        print(a) // a Reference Count 1+1 == 2
      }
    } // a Reference Count 2-1 == 1
    ~~~

- weak 
  - 객체가 할당 될 때 RC를 증가시키지 않는다. 또한 weak 키워드는 Optional에만 적용이 된다. ARC에 의해 AC가 0이 되면 해당 메모리는 해제되고 nil이 된다. 
  - 클로저 내 상호참조로 인한 Closure Capturing을 해결할 수 있는 방법 중 하나이다. 
  - 비교적 Life Cycle이 짧은 경우에 사용한다. 

- Unowned
  - 객체가 할당 될 때 RC를 증가시키지 않는다. 그러나 weak 멤버와 달리 Non-Optional로 선언되어야 하며, ARC에 의해 메모리 해제가 된 후에도 해당 메모리의 값을 있는것으로 인지하며 이 상황에 해당 메모리를 참조할 경우 앱 크래시가 발생할 수 있다. 
  - 해당 객체의 Life Cycle이 명확하고 개발자에 의해 판단이 서는 경우, weak 대신 사용하여 옵셔널 바인딩 등의 과정을 거치지 않고 보다 간결한 코딩이 가능해진다. 



#### - Weak, unowned의 용도와 차이점

- weak은 해당 값이 nil일 수도 있어 nil일 경우 해당 내용을 실행하지 않음으로서 클로져 캡쳐링을 방지한다. 
  - ARC 카운트가 0이 되면 nil로 바꿔주는 런타임 작업이 존재한다.
- unowned는 해당 멤버가 반드시 존재한다고 가정, 만약 힙에 해당 멤버가 없으면 런타임 중 앱 크래시를 발생시킴으로서 클로져 캡쳐링을 방지한다.
  - weak와 달리 unowned에서는 ARC 카운트가 0이 되면 nil로 바꿔주는 런타임 작업이 않는다.

<br><br>

### # IBOutlet의 weak 사용 여부 문제

- iOS6 버전 까지는 앱 실행 간 메모리 부족문제가 발생할때 시스템이 임의로 viewWillUnload, viewDidUnload 함수를 사용하여 뷰를 해제했으나 이때 @IBOutlet 멤버의 경우 weak 설정이 되지 않으면 시스템이 뷰를 해제했으나 사용하지 않는 뷰가 ARC 해제되지않고 남아있게 되는 문제가 있을 수 있었다.
- iOS6 이후부터는 시스템이 뷰의 해제에 임의로 관여하지 않고 대신 개발자가 didReceiveMemoryWarning()에서 메모리 부족 상황의 작업을 처리할 수 있게 됨으로서 @IBOutlet의 별도 weak 설정이 필요없게 되었다. 
- 그렇게 시스템이 메모리 부족 상황에 대한 임의적 뷰 메모리 해제에 관여하지 않게 됨으로서 뷰 헤제에 시스템이 사용하던 viewWilllUnload / viewDidUnload는 필요없게 되었다. (deprecated)

<br><br>

### # Escaping Closure의 개념 

- 메서드로 부터 전달받은 closure를 메서드의 LifeCycle에서 실행하여 끝내지 않고 closure 내부의 결과를 외부에 전달하고자 할 때 사용할 수 있다.
  - 콜백함수 같은 효과를 볼 수 있음
- 해당 메서드의 호출이 끝난 이후에도 closure는 메모리 어딘가에 저장되어 있어야하는데 이때 상황에 따라 weak 멤버등의 사용이 필요할  수 있음을 고려해야한다. 
- @escaping이 명시되어있지 않은 경우 일반적으로 non-escaping closure이며, 메서드 실행의 종료 이전에 closure의 사용이 모두 완료됨을 보장할
  - Non-escaping closure의 경우 weak 없이도 안전하게 사용할 수 있다. 

<br><br>

### # as, as?, as! 의 차이

- as
  - 컴파일러가 타입의 성공을 보장하는 타입캐스팅 방법
  - 컴파일 타임에 캐스팅 가능/불가능 여부를 확인 가능하다.
- as? 
  - 타입 변환에 실패할 경우 nil을 리턴한다. 
  - 컴파일 타임에 캐스팅 가능/불가능 여부를 확인 불가(Xcode IDE에선 가능)

- as!
  - 타입 변환에 실패할 경우 앱 크래시가 발생한다. 
  - 컴파일 타임에 캐스팅 가능/불가능 여부를 확인 불가(Xcode IDE에선 가능)
- ☆ Xcode 등의 일부 IDE에서는 정적 코드검사를 통해 as, as?, as! 모두에 대한 warning을 제공한다. 

<br><br>



### # Swift에서의 Class - Struct의 차이

- **Class**
  - 참조 타입 (Reference Type)
  - 객체로 사용 시 메모리 영역에 서상되며 ARC체계로 메모리 해제가 이루어진다. 
  - 멀티스레딩, 클로저 내 참조 시 ClosureCapturing 등의 메모리 순환에 주의해야 한다.
  - 공짜 이니셜라이저가 존재하지 않는다. 
  - 상속, 프로토콜 채택이 가능하다. 
  - let으로 Class 객체 생성을 했어도 객체를 접근해서 객체 내의 variable 멤버의 값을 변경시킬 수 있다.
  - Struct에서 사용할 수 있는 mutating 키워드를 사용할 필요가 없다. 
- **Struct**
  - 값 타입 (Value Type)
  - Struct는 대입 연산 시 값 자체가 복사되어 할당되며 원본과 공유가 불가능하다. 
  - 불변성(Immutable) 구현에 유리
  - 멀티스레딩에 안전하다.
  - 공짜 이니셜라이저(자동 생성자)가 존재한다. 
  - 상속이 불가능, 프로토콜 채택만 가능하다. 
  - let으로 Struct 객체를 생성하면 객체 내의 멤버가 variable이어도 해당 멤버의 값을 변경시킬 수 없다. 
  - 객체 내의 변경을 요구하는 경우 mutating 키워드를 사용해서 메서드를 정의한다. 



<br><br>

### # 익스텐션 Extension

- **인스텐션은 iOS에서 매우 강력한 도구**이다.
- **extension은 저장공간이 있는 변수는 아니다.** 
- **extension은 간편하여 쉽게 사용**될 수 있다.
  - 그러나 **extension사용 시 불필요한 기능인지 고려할 필요**가 있다.

~~~ swift
// extension 사용 예시)
extension UIView {
  	// UIView 객체의 추가적인 사용자 정의 메서드를 정의할 수 있다. 
  	func configureDefaultView() {
      	self.background = .black
    }
}
~~~



<br><br>

### # 프로토콜 Protocol

- **Struct, Class , Enum과 함께 스위프트의 자료구조를 형성하는 네번째 기둥**
  - **별도의 세부 구현이 없는 메서드, 프로퍼티로 구성하고 있는 하나의 일급 타입**
  - **실제 구현이 아닌 순수한 선언형태**를 갖고 있다. 
  - **class만 취급하는 프로토콜의 경우 : class로 class에서만 사용하도록 지정할 수 있다.** 
- Swift 내 문자열, 배열 등 많은 것들이 프로토콜을 사용하고 있으며, 이들의 기초가 되고 있다.
- 다중상속을 지원하지 않는 Swift에서 **다중상속과 같은 효과, Controller-View 간 Delegation 블라인드 소통 기능** 등 다양한 곳에 사용할 수 있다. 

~~~ swift
// 프로토콜의 선언 예시)
protocol AProtocol: InheritedProtocolA, InheritedProtocolB {
  	var someProperty: Int { get set } // 읽기(get), 쓰기(set)이 가능한 가변 프로퍼티, someProperty
  	func aMethod(arg1: Double, anotherArgument: String) -> SomeType
  	optional func optionMethod() // protocol 메서드 앞에 optional을 붙여주면 해당 프로토콜을 채택받아도 해당 메서드를 선택적으로 구현할 수 있도록 할 수 있다. 
  	mutating func changeIt() // 만약 : class를 AProtocol에 붙여주면 mutating을 붙여줄 필요가 없어진다. 
  	init(arg: Type)
}
~~~

<br>



### ## 주요 프로토콜 종류

- Hashable

  - Hash값을 제공하는 타입 
  - Dictionary의 KeyType은 Hashable 프로토콜을 준수하는 값만 사용 가능하다. 
  - Set 타입은 Hashable 프토토콜을 준수한 값만 사용 가능하다. 
  - Hashable 프토토콜을 준수하기 위해서는 ==연산자, hashValue프로퍼티를 제공해야 한다. 

  ~~~ swift
  extension ToAdjustHash: Hashable {
      // hashValue 계산 프로퍼티의 정의
    	var hashValue: Int {
  				return x.hashValue ^ y.hashValue &* 1675827
      }
    	
      // == 연산자의 정의
    	static func == (lhs: GridPoint, rhs GridPoint) -> Bool {
        	return lhs.x == rhs.x && lhs.y == rhs.y
      }
  }
  ~~~

  

<br>







<br><br>

### # 열거형 Enum

- Class, Struct와 더불어 **Swift 데이터 구조의 일종인 Enum**
- Struct와 동일한 **값 타입의 데이터 타입**
- 메서드, 변수 등을 가질 수 있지만 연동자료 따로 갖고 있지는 않다.
  - enum 내 연동자료들을 제외하고는 저장공간을 갖고 있지 않다.
  - **case let 을 통해 enum case에 따른 연동자료를 얻도록 할 수 있다.** 
- **Swift의 enum은 다른 언어에 비해 매우 강력**하다. 
  - **enum 각각의 case들이 연동된 데이터 값을 가질 수 있기 때문**이다. 
  - Optional도 none, some의 case로 이루어진 enum으로 구성되어진다. 

~~~ swift
// enum의 멤머 프로퍼티 + switch self를 활용한 case 별 연동자료 흭득 에시
enum Food {
    case banana(Int)
    case icecream(Int)
    case potato(Int)
    
    // enum case에 따른 내의 저장프로퍼티(price)의 값을 다양하게 줄 수 있다.
    var price: Int {
        // 인자값에 따른 케이스 별 연동자료를 반환받을 수 있다.
        switch self {
        case let .banana(value):
            return value*10
        case let .icecream(value):
            return value*3
        case let .potato(value):
            return value*5
        }
    }
}

// 같은 enum 타입의 객체라도 rawValue 값에 따른 연동자료의 결과값이 다양하게 나올 수 있다.
var icecream: Food = Food.icecream(3) // return 3 * 3
var potato = Food.potato(6) // return 6 * 5
var banana = Food.banana(2) // return 2 * 10
print("total icecream price : \(icecream.price)") // 9
print("total potato price : \(potato.price)") // 30
print("total banana price : \(banana.price)") // 20
~~~

<br><br>



### # Frame - Bounds의 차이

- Frame
  - SuperView(상위뷰) 좌표 시스템 내에서의 View 위치(origin)와 크기(size)
- Bounds
  - view 자기자신을 기준으로 한 좌표시스템에서의 위치(origin)와 크기(size)
    - 기본적인 default origin은 x:0, y:0을 가리킨다. 
  - 부모 뷰의 위치관계와는 아무런 관계가 없다. 
  - bounds 값이 변경되면 해당 뷰의 서브뷰들의 드로잉 위치가 변경됨을 의미한다. 
  - bounds값이 변경될 때 subView의 위치가 바뀌는 것은 subView의 frame값이 변경된 것이 아니다. 
    - bounds값이 바뀌면서 해당 뷰의 좌표축이 변경되었기 때문에 그에따라 서브뷰의 드로잉 위치가 변경되는 것일 뿐이다. 
  - Bounds 실 사용 예시
    - UIScrollView/UITableView 등을 스크롤 할때 scrollView.bounds가 변경됨으로서 subView들의 위치가 달라지는 것인 bounds 특징의 예이다. 
    - 이때도 subView들의 frame은 변동되지 않는다. 



<br><br>

### # UIViewController 프로퍼티인 TopLayoutGuide, BottomLayoutGuide가 iOS11에서 deprecated된 이유와 대체수단

- 아이폰X가 생기면서 안전영역에 대한 **SafeAreaLayoutGuide**가 생겼기 때문이다.
  - **SafeAreaLayoutGuide**는 기존 Top, Bottom LayoutGuide와 **다르게 안전한 컨텐츠 영역의 개념**으로 등장했다.
- 기존 TopLayoutGuide, BottomLayoutGuide는 두개의 사각 영역으로 되어있는 GuideArea였던 반면, SafeAreaLayoutGuide는 좌/우/위/아래의 하나의 사각 영역으로 되어 있다. 



<br><br>



### # Timer 

- 일정 주기마다 특정한 작업을 처리하기 위해 사용할 수 있음
- scheduledTimer(withTimeInterval:, repeats:) { timer in ... } 
  - 일정 주기별로 작업을 실행할 때 사용한다. 
- 런루프에 등록이 되어 실행되며, invalidate 될 경우 nil이 되며 헤제된다. 
- 만약 **타이머가 nil인데 fire()함수로 타이머를 사용하려고 하면 앱크래시가 발생할 수 있다.** 
  - 그러므로 **이런 부분의 안정성을 확보하기 위해 weak키워드를 사용하는 것이 좋다.** 





<br><br>

### # UIStackView의 장점 

- **복잡한 제약 설정 없이 비교적 간단하게 복잡한 뷰 구조를 구현**할 수 있다. 
- **arrangedSubview로 UIStackView의 subView들이 관리**되며 하위뷰를은 UIStackView의 **alignment(세로방향), distribution(가로방향), Axis(가로/세로 기준), spacing(subView 간 간격)**의 규칙에 의해 위치가 지정된다. 



<br><br>



### # AutoLayout Constraint, Priority의 개념

- 이름 그대로 AutoLayout 간 제약, 우선순위값을 의미한다. 
  - 일반적으로 제약 간의 충돌이 일어나지 않게 제약을 설정해야하나, 상황에 따라 뷰의 크기가 유동적으로 변하는 경우가 있을 수 있다. 
  - **이런 제약값이 서로 충돌날 수 있는 경우가 있을때의 우선순위를 결정함으로서 제약의 충돌을 방지**할 수 있게 된다. 

<br><br>

### # Intrinsic Content Size

- **UI FrameWork에서 제공되는 일부 View는 고유 컨텐츠사이즈(Intrinsic Content Size)를 가지고 있으며 그 예는 UILabel, UIButton** 등이 있다. 
  - UILabel, UIButton 등은 뷰의 속성(텍스트, 이미지)에 따라 크기가 결정 될 수 있는데 이 때 Intrinsic Content Size보다 작아지거나 커질 수가 있다. 
  - **일반 Contraint Priority** 
    - **Leading, Trailing, Top, Bottom, Width, Height 등의 Contraints가 존재**
    - **기본 값 1000**
  - **Content Hugging Priority**
    - **최대 크기에 대한 제한 우선순위, ** **기본 값 250**
      - **"주어진 크기보다 Hugging Priority 순위에 따라 작아질 수 있음"**
      - **Q) 두 개의 별도의 width값은 없는 라벨**이 **Hugging Priority 250, 어느하나의 Hugging Priority 값이 251이 되면?**
        - **Hugging Priority 250 Label**  **→ 현재 크기보다 라벨 크기가 늘어난다.(Hugging에 의한 작아질 수 있는 제한이 풀렸으므로...)**
        - **Hugging Priority 251 Label** → **Intrinsic Content Size 이상의 크기 범위 내에서 현재 크기보다 줄어들 수 있다.**
  - **Content Compression Resistance**
    - **최소 크기에 대한 제한 우선순위,** **기본 값 750**
      - **"주어진 크기보다 Compression Resistance 순위에 따라 커질 수 있음"**
    - **크기가 줄어드는 것에 대해 저항하는 제약 값** 이라고 한다. 

<br><br>



### # iOS 디바이스 크기를 확인하는 법

- 디바이스 크기마다 개발자가 일일히 체크하고 세세하게 코딩하기란 쉽지않다.
  - 이 문제를 해결하기 위해 **iOS에서는 기종에 따라 카테고리를 분리하여 대응할 수 있도록 제공**하고 있다.

#### ## UITraitEnvironment

- **앱에 대한 iOS 인터페이스 환경을 구성해줄 수 있는 메서드의 집합이 정의되어 있는 프로토콜**
- **UIScreen, UIWindow, UIViewController, UIPresentationController, UIView 등이 UITraitEnvironment 프로토콜을 채택해서 사용**한다. 

#### ## Size Class

- **UITraitEnvironment 프로토콜을 채택한 클래스의 traitCollection프로퍼티로 접근하여 기기의 카테고리를 식별**할 수 있다. 
  - **UIScreen, UIWindow, UIViewController, UIPresentationController, UIView 등을 통해 접근 가능**
- **사이즈 클래스는 regular, compact로 분류되며 기기의 종류 / 가로세로 방향에 따라 정해진다.**
  - **아이패드 : Portrait & Landscape : R/R**
  - **아이폰+ : Portrait : C/R, Landscape : R/C**
  - **아이폰 : Protrait : C/R, Landscape : C/C**



<br><br>



### # UICollectionViewLayout클래스의 prepare 메소드 역할

- **prepare 메서드는 UICollectionView의 Layout 연산이 일어날 때마다 호출**된다. 이때 셀 위치, 크기등에 대한 계산을 prepare 메소드에서 사전에 할 수 있다.
- 

<br><br>

### # UITableView 구성 시 셀 컨텐츠에 따른 높이 설정을 하는 방법

- **UITableViewDelegate 프로토콜을 채택해여 델리게이트 메서드인 heightForRowAt 메서드에서 UITableView.automaticDimension값을 리턴**하면 된다. 
- 세부적으로 셀의 최소 높이 등을 에측하기 위해서는 UITableView의 estimatedRowHeight 등의 프로퍼티를 설정해주면 된다.

<br><br>



### # appDelegate의 keyWindow 유무

- **iOS12 까지는 AppDelegate의 단일 keyWindow 방식**을 갖고 있었다. 
- -> **iOS13 부터는  appDelegate에만 단일 keyWindow를 갖고 있던 방식에서 SceneDelegate가 추가되면서 SceneDelegate 각각의 keyWindow**를 갖고있게 되었다.





<br><br>

### # GCD란?, 사용법

- **GCD (Grand Central Dispatch)**
  - DispatchQueue
  - Queue와 동일하게 FIFO의 특징을 갖고 있다. 
  - qos (qualify of service)
    - userInteractive
    - userInitiated
    - Default
    - utility
    - backgound
    - Unspecified
- **Serial**
  - 한번에 하나의 작업만 하는 queue
  - 앞선 작업이 완전히 종료 되어야지만 다음 작업이 순차적으로 실행된다. 
- **Concurrent**
  - 동시에 여러작업을 수행하는 queue
  - 앞선 작업이 실행되는 도중에도 뒤의 큐 작업이 동시에 실행된다. 
- **DispatchQueue 사용 예시**

~~~ swift

// dispatchQueue test 
let dispatchQueue = DispatchQueue(label: "min") // serial DispatchQueue 
let dispatchQueue2 = DispatchQueue(label: "mingoon", attributes: .concurrent) // concurrent DispatchQueue

// main 스레드에서 동작하는 비동기 DispatchQueue
DispatchQueue.main.async {
    print("mainQueue")
}

// 서브 스레드에서 작동하는 serial DispatchQueue
// 다른 serial async 블록과의 관계 -> 블록 순차적으로 실행
dispatchQueue.async {
    // 스레드 8에서 작동
    print("serial async")
}

// 서브 스레드에서 작동하는 concurrent DispatchQueue
// 다른 concurrent async 블록과의 관계 -> 앞선 블록 작업 종료와 관계없이 동시에 실행 
dispatchQueue2.async {
    // 스레드 3에서 작동
    print("concurrent async")
}
~~~



<br><br>



### OperationQueue란?, 사용법 

- Cocoa operation은 비동기적으로 수행하고자 하는 작업을 캡슐화하는 객체지향적 방법(object-oriented way)이다.
- **Objective-C 기반으로 OS X 및 Cocoa 기반 앱에서도 사용 가능**하다. 
- **OperationQueue는 DispatchQueue보다 좀더 객체 지향적인 비동기 프로그래밍을 구현해야할 때 사용**한다. 
- **Operation 작업 간 각각 or 전체 Operation에 대한 전체 실행취소가 가능**하다. 
  - **개별 Operation 취소 : cancel()**
  - **전체 Operation에 대한 작업 취소 : cancelAllOperation()**

- **OperationQueue의 사용방법**

~~~ swift
let queue = OperationQueue() // OperationQueue의 생성 및 할당 
queue.addOperation {
  	for index in 1...100 {
      	print("applebuddy\(index)") // prints 1...100
    }
}
~~~



<br><br>



### Core Graphics 란, 구성 요소

- **Core Graphics의 의미**

  - **iOS 뷰의 색상, 이미지, 그레디언트, 그림자, 레이어효과등을 내는데 처리하는데 사용**한다. 
  - **좌표계 체계 데이터 구조, Coordinate System Data Structures**

- **Core Graphics의 구성 요소**

  - **CGFloat** 

    - **드로잉 간 부동 소수점 좌표를 나타내는 기본타입**
    - **드로잉을 하는 모든 지점은 모두 부동 소수점으로 표현**되며 이때 CGFloat타입을 사용한다. 

  - **CGPoint**

    - **두 개의 CGFloat 변수 x, y로 구성되는 구조체 타입**
    - **CGFloat 기반 좌표로 점의 위치를 표현하는데 사용**한다. 

  - **CGSize**

    - **두 개의 CGFloat 변수 width, height로 구성되는 구조체 타입**
    - **CGFloat 기반으로 크기를 표현하는데 사용**한다. 

  - **CGRect**

    - **점(CGPoint)과 크기(CGSize)를 조합해서 구성한 구조체 타입**
    - **CGPoint, CGSize를 함께 갖고 있다.** 

    ~~~ swift
    // CGRect 구조체 구조
    struct CGRect {
      	var origin: CGPoint // 좌표를 표현하는 origin: CGPoint
      	var size: CGSize // 크기를 표현하는 size: CGSize
    }
    ~~~



<br><br>



### # associatedtype 

- 일반적으로 변수가 특정 자료형으로 선언되면 그 이외의 자료형으로 동적으로 타입이 변할 수 없다. 
  - 이때 타입을 동적으로 사용할 수 있도록 해주는 건이 associatedtype이다. 
- associatedtype의 사용 예시)

~~~ swift
protocol B {}
extension B {
  	var description: String {
      	return "Hello World"
    }
}

protocol C {}
extension C {
		var debug: String {
			return "Debug"
    }
}

protocol A {
  	associatedtype T: B, C // associatedtype을 사용해 B, C 프로토콜을 모두 준수하는 타입을 정의한다.  
  	var name: T { get set } // protocol의 정의 프로퍼티 name은 B, C 프로토콜을 준수하는 + 읽기/쓰기가 가능한 T 타입으로 정의 된다.
}
 
extension A {
  	mutating func set(name: T) {
      	self.name = name
    }
  
  	// T타입으로 정의 된 name은 프로토콜 B, C의 메서드를 모두 사용할 수 있다. 
  	var desctription: String {
      	return name.description
    }
  
    var debug: String {
      	return name.debug
    }
}
~~~



<br><br>



### # Collection 종류

- BiDirectionalCollection
  - 양방향 컬렉션
    - count 속도가 랜덤 접근 컬렉션보다 느리다. **복잡도 O(N)**
  - swift의 String 자료형에 사용된다.

- RandomAccessCollection
  - 랜덤 접근 컬렉션
    - count 속도가 복잡도 **O(1)**
  - swift의 배열, C++의 벡터, 배열 등에 사용한다. 

<br>



### Static Dispatch, Dynamic Dispatch

- iOS의 Swift 또한 다른 객체지향 언어들처럼 오버라이딩을 지원한다. 오버라이딩을 할때 프로그램을 실제 호출할 함수가 어떤 것인지를 결정하는 과정이 필요하다.

~~~ swift
class Parent {
  	func someMethod() {
      	// 부모 클래스의 someMethod 메서드 구현 
    }
}

class Child: Parent {
  	override func someMethod() {
      	// 자식 클래스의 someMethod 메서드 구현
    }
}

let object: Parent = Child()
object.someMethod() 
// 이때 Parent의 someMethod를 호출할 것인가, Child의 someMethod를 호출할 것인가?
// 그 여부는 Static Dispatch(Direct Call) vs Dynamic Dispatch(Indirect Call) 여부에 따라 결정 된다. 
~~~

<br>

- **Static Dispatch** (Direct Call)
  - **Static Dispatch 방법은 변수의 명목상 타입을 기준으로 메소드와 프로퍼티를 참조**한다. 
  - **참조할 요소를 컴파일 타임에 결정하므로 성능상의 이점**을 갖는다. 
  - 자식클래스의 오버라이딩 메서드를 호출하려면 명시적인 타입 캐스팅을 해주어야 한다.
    - ex) **C++의 경우 정적바인딩이 원칙**이므로 **virtual 키워드를 사용해야만 서브클래스의 오버라이딩 메서드를 사용 가능**하다. 
    - **다형성을 활용하기 어려운 단점**이 있다. 

- **Dynamic Dispatch** (Indirect Call)
  - **Swift에서 채택해서 사용하는 Dynamic Dispatch 방식**
  - **변수의 실제 타입에 맞춰서 메서드와 프로퍼티를 호출**한다.
  - **실제 참조 될 요소는 런타임 중에 결정**된다.
  - **어떤 서브클래스에 접근해도 실제 타입에 맞는 요소를 참조하여 실행하기 때문에 다형성 구현에 용이**하다.
  - **런타임 중 작업이 있으므로 Static Dispatch에 비해 성능상으론 손해보는 단점**이 있다.



<br>



<br>

### # 예약어 문법

- **Defer**

  - 해당 블럭을 벗어날 때 실행할 작업을 블록  내에서 앞서 지정할 수 있다. 

  ~~~swift
  // defer 활용 예시)
  func deferTest() {
    	defer { print("3") }
    	print("1")
    	print("2")
  }
  
  defer() // "1" \n "2" \n "3"
  ~~~

- **Assert**

  - **디버깅 모드에서 특정 조건을 만족시키는지 확인 후, 조건을 성립하지 않으면 크래시를 발생**시킨다.
  - **디버깅 모드에서만 동작하며 애플리케이션에서는 해당 내용을 제외**한다.
    - **배포 환경에서도 동작하는 메서드는 precondition(_:file:line:)** 이 있다.

  ~~~ swift
  // Assert 활용 예시)
  var someInt: Int = 0
  
  // Assert를 사용해 검증 조건을 체크한다. 문제가 없으면 그대로 행을 지나간다. 
  assert(someInt == 0, "someInt is Not a Zero!!")
  // Assert로 조건 검증 시 문제가 있으면 문구를 출력하고 동작 중지
  assert(someInt != 0, "someInt is a Zero!!")
  
  ~~~

  