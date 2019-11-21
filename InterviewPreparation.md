# 면접 질문 정리 

- 면접에 나올 수 있는 기초 질문에 대한 답변 정리
- by applebuddy



<br><br>

# @ 공통 질문



### # 자기소개





<br><br>

### # 마지막으로 하고싶은 말





<br><br>



# @ CS 기술 질문

### Sorting Methods, 정렬 방법

- **퀵 정렬 (Quick Sort)**
  - 일반적으로 좋은 성능을 보이는 정렬방법, 비펏을 기준으로 비벗보다 작은값, 큰값을 양옆으로 비교하며 재귀, 분할정복방식으로 정렬을 수행한다. 
  - **최적의 상황에서 복잡도는 O(NlogN)** 이다.
    - 분발정복 알고리즘이 적용되어 정렬 체크구간이 쪼개질 수록 복잡도가 줄어든다.
  - **최악의 상황에서 복잡도는 O(N^2)** 이다.
    - **이미 정렬이 되어있는 상태에서 비펏이 양 끝에 위치할 경우 N^2번을 순회**하며 분할정복의 이점을 활용하지 못하기 때문이다. 
- **게수정렬(Counting Sort)**
  - 계수가능 범위에서 배열 인덱스를 이용해 요소를 정렬한다. 
  - **복잡도는 O(N)로 매우 효율적**이다.
  - **일정 이상의 계수범위를 넘어갈 시 메모리의 과부하가 발생**할 수 있다. 
    - 매우 큰 계수 범위에 대한 사용 제한
- **힙 정렬 (Heap Sort)** 
  - Complete Binary Tree를 이용한 Heap 정렬
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



#### ARC 란 무엇인가요?

- ARC는 Automactic Reference Counting의 약어이다.
- ARC는 컴파일 시점에 동작하며 코드를 빌드(컴파일) 할 때 객체의 RC(Reference Count)를 추척하여 0이 되는 시점에는 자동으로 release 코드를 넣어 해제해주는 방식을 말한다. 

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



### # UIViewController 프로퍼티인 TopLayoutGuide, BottomLayoutGuide가 iOS11에서 deprecated된 이유와 대체수단

- 아이폰X가 생기면서 안전영역에 대한 **SafeAreaLayoutGuide**가 생겼기 때문이다.
  - **SafeAreaLayoutGuide**는 기존 Top, Bottom LayoutGuide와 **다르게 안전한 컨텐츠 영역의 개념**으로 등장했다.
- 기존 TopLayoutGuide, BottomLayoutGuide는 두개의 사각 영역으로 되어있는 GuideArea였던 반면, SafeAreaLayoutGuide는 좌/우/위/아래의 하나의 사각 영역으로 되어 있다. 



<br><br>

### # UIStackView의 장점 

- **복잡한 제약 설정 없이 비교적 간단하게 복잡한 뷰 구조를 구현**할 수 있다. 
- **arrangedSubview로 UIStackView의 subView들이 관리**되며 하위뷰를은 UIStackView의 **alignment(세로방향), distribution(가로방향), Axis(가로/세로 기준), spacing(subView 간 간격)**의 규칙에 의해 위치가 지정된다. 



<br><br>



### # AutoLayout Constraint, Priority의 개념

- 이름 그대로 AutoLayout 간 제약, 우선순위값을 의미한다. 
  - 일반적으로 제약 간의 충돌이 일어나지 않게 제약을 설정해야하나, 상황에 따라 뷰의 크기가 유동적으로 변하는 경우가 있을 수 있다. 
  - 이런 제약값이 서로 충돌날 수 있는 경우가 있을때의 우선순위를 결정함으로서 제약의 충돌을 방지할 수 있게 된다. 

<br><br>

### # Intrinsic Content Size

- **UI FrameWork에서 제공되는 일부 View는 고유 컨텐츠사이즈(Intrinsic Content Size)를 가지고 있으며 그 예는 UILabel, UIButton** 등이 있다. 
  - UILabel, UIButton 등은 뷰의 속성(텍스트, 이미지)에 따라 크기가 결정 될 수 있는데 이 때 Intrinsic Content Size보다 작아지거나 커질 수가 있다. 
  - 이때 **Content Hugging Priority는 크기가 늘어나는 것에 대해 저항하는 제약값, Content Compression Resistance는 크기가 줄어드는 것에 대해 저항하는 제약값** 이라고 한다. 
  - **Content Compression Resistance - Content Hugging Priority - Autolayout Constraint 간에도 우선순위가 존재**하는데 이 중 **Autolayout Constraint Priority가 최우선순위로 적용**된다. 

<br><br>

### # UICollectionViewLayout클래스의 prepare 메소드 역할

- **prepare 메서드는 UICollectionView의 Layout 연산이 일어날 때마다 호출**된다. 이때 셀 위치, 크기등에 대한 계산을 prepare 메소드에서 사전에 할 수 있다.

<br><br>

### # UITableView 구성 시 셀 컨텐츠에 따른 높이 설정을 하는 방법

- **UITableViewDelegate 프로토콜을 채택해여 델리게이트 메서드인 heightForRowAt 메서드에서 UITableView.automaticDimension값을 리턴**하면 된다. 
- 세부적으로 셀의 최소 높이 등을 에측하기 위해서는 UITableView의 estimatedRowHeight 등의 프로퍼티를 설정해주면 된다.

<br><br>



### # GCD의 사용법

- GCD (Grand Central Dispatch)
  - DispatchQueue

