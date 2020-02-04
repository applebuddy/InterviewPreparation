****

# 면접 질문 정리 

- 면접에 나올 수 있는 기초 질문에 대한 답변 정리
- by applebuddy



<br><br>

# @ 공통 질문



### # 자기소개


<br><br>

### # 마지막으로 하고싶은 말

.



<br><br>

### # 성취 해본 가장 인상적인 경험





<br><br>




# @ iOS 동향 질문

- **iOS13 버전의 중요 업데이트 내용**
  - **다크모드 (DarkMode) 지원**
  - **사진앱의 AI기술을 활용한 정렬기능 도입**
    - 사진 간 연관성 분석을 하여 사용자에게 알맞는 정렬을 보여주도록 함
    - 사진들을 분석해서 연도별, 테마별 인생에서 가장 중요한 순간들을 정리하여 분류
  - **애플 소셜 로그인 지원**
    - **애플 소셜 로그인 API 공개**
    - 로그인을 시도하면 별 다른 입력 절차 없이 Face ID를 이용해서 로그인이 가능, 세부 개인정보 공개 설정이 가능하다.
  - **씬델리게이트 (SceneDelegate) 추가** 
  - **Opaque type (불투명 타입), property Wrapper (프로퍼티 래퍼) 추가**

<br>

- **OpaqueType**

  - **Swift 5.1버전으로 추가 된 Opaque Type (불투명 타입)**
  -  **프로토콜 명을 some 뒤에 선언하여 구체적인 반환타입을 숨길 수 있도록 해준다.** 

~~~ swift
// makeCollection Method는 return 타입으로 구체적 타입을 지정하지 않고 Collection 프로토콜을 준수하는 타입이라는 것만 명시해줄 수 있다. 
// -> OpaqueType을 사용하여 구체적인 타입을 숨길 수 있다. -> 말 그대로 불투명 타입
func makeCollection() -> some Collection { 
return [1, 2, 3]
}
~~~

<br><br>

# @ Objective-C 관련 질문

## KVC
- **참고 링크: https://jcsoohwancho.github.io/2019-11-28-Key-Value-Coding(KVC))**
- **KVC는 특정 객체에 문자열(Key)를 이용해서 해당 객체의 프로퍼티 값(Value)에 간접적으로 접근하게 만들어주는 Objective-C 기술** 중 하나이다. 
- KVC를 적용한 객체는 Objective-C에서의 메소드 호출 방식인 메시징 인터페이스로 일원화시킬 수 있다. 
- KVC는 Objective-C RunTime에 의존하는 기술이기 떄문에 Swift에서 KVC를 사용하기 위해서는 해당 객체가 NSObject를 상속받은 클래스여야 하며, KVC를 적용하려는 프로퍼티에 @objc Annotation을 붙여서 해당 프로퍼티를 Objective-C RunTime에 노출시켜야 한다. 
- **KVC 적용예시 ▼**
~~~ swift
class Derived: NSObject {
    @objc let x: Int
    override init() {
    	x = 1
	super.init()
    }
}

let derived = Derived()
print(derived.value(forKey: "x")) // Optional
~~~
<br>

### KVC 사용하기
- KVC를 활용하기 위해서는 NSObject를 상속 받아야 하고, 원하는 프로퍼티를 Objective-C RunTime에 노출시켜야 한다. 
  - NSObject를 상속받은 객체에서 KVC를 사용하기 때문에 KVO와 마찬가지로 클래스에서만 적용하여 사용할 수 있다.



## KVO 
- **참고 링크: https://jcsoohwancho.github.io/2019-11-30-KVO(Key-Value-Observing)**
- **Key Value Observing으로 객체의 프로퍼티 변화를 감시하고, 변화할때에 맞춰서 필요한 동작을 수행**할 수 있도록 한다. 
- swift언어와 함께 KVO를 사용하기 위해서는 관련된 객체 모두가 KVO를 지원해야한다.
  - 이를 위해서는 NSObject를 상속해야하며 이는 곧 클래스만 KVO를 구현할 수 있음을 의미한다. (구조체, 열거형 등은 구조체타입으로 상속이 불가능하기 때문)
- 변화를 감지하기위한 프로퍼티에 dynamic 키워드를 붙여주어야한다. 
  - dynamic 키워드를 붙여 해당 프로퍼티를 Objective-C Runtime에 노출시키고 Message Dispatch를 사용할 수 있도록 한다. 
  - @objc Annotation을 붙여도 dynamic을 붙이지 않으면 KVO기능을 사용할 수 없다. 

<br>

### KVO 적용할 프로퍼티 선언
- **KVO 적용할 프로퍼티 선언하기 ▼**
~~~ swift
import Foundation 

// KVO사용을 하려는 객체는 NSObject를 상속받은 클래스여야 한다. 
class Derived: NSObject {
    // KVO를 사용하고자 하는 프로퍼티에 @objc dynamic 키워드를 붙여서 KVO를 사용한다.
    @objc dynamic var rect: CGRect = CGRect(x: 0, y: 0, width: 0, height: 0)
}
~~~
<br>

### Observer 등록
- addObserver(_:forKeyPath:options:context:) 메소드를 통해서, Observer를 등록한다. 
- forkeyPath: String타입으로 감지하고자 하는 프로퍼티를 지정한다. 
- options: 지정한 프로퍼티의 값이 변화할 대, 어떤 시점의 값을 돌려받을 지 지정한다. 다수의 옵션을 지정할 수도 있다. 
  - .old : 변경 이전 값을 dictionary에 담으며 oldKey로 참조할 수 있다.
  - .new : 새로 변경된 값을 dictionary에 담는다. newKey로 참조할 수 있다. 
- Observer로 사용될 객체는 observeValue(forKeyPath:of:change:context)를 오버라이드 해야한다. 
- **KVO 프로퍼티에 옵저버 추가 + observeValue override 하기 ▼**

~~~ swift 
class Observer: NSObject {
    let derived = Derived()
    
    override init() {
    	super.init()
	// NSObject를 상속받은 클래스 인스턴스의 rect프로퍼티를 감지하기 위해 옵저버를 추가하고 있다.
	derived.addObserver(self, forKeyPath: "rect", options: [.new, .old], context: nil)
    }
    
    // 옵저버 역할을 하는 객체는 observeValue 메서드를 override하여 프로퍼티 변화를 감지할 수 있다.
    override func observeValue(forKeyPath keyPath: String?, of object: Any? change: [NSKeyValueChangeKEy : Any]?, context: UnsafeMutableRawPointer?) {
    	if let old = change?[.oldKey] as? CGRect,
	let new = change?[.newKey] as? CGRect {
	    print("\(old) -> \(new) updated!!")
	}
    }
}
~~~

<br>


### KVO 제외(옵저버 삭제)하기 
- 특정 감시를 중단하고 싶다면, removeObserver로 Observer를 제거할 수 있다. 
~~~ swift
removeObserver(_:forKeyPath:)
~~~

<br>

### KVO와 유사한 swift 기능, PropertyObserver
- Swift에서는 KVO와 비슷한 역할을 수행할 수 있는 Property Observer를 제공한다. 
- KVO와 비슷하지만 NSObject를 상속받지 않는 값 타입에도 적용될 수 있다는 장점이있다. 
- Property Observer는 타입선언의 일부로서 컴파일 타입에 지정되며 정적인 반면, KVO는 런타임에 동적으로 추가되는 것이라는 차이점이 있다. 
- **Swift PropertyObserver 활용 예시 ▼**
~~~ swift
struct Observer {
    var rect: CGRect {
    	willSet {
	    print("\(self.rect) will change to \(newValue)")
	}
	
	didSet {
	    print("\(oldValue) changed to \(self.rect)")
	}
    }
    
    mutating func changeValue(_ new: CGRect) {
    	rect = new
    }
}	

var observer = Observer(rect: CGRect(x: 0, y: 0, width: 0, height: 0))
observer.changeValue(CGRect(x: 0, y: 0, width: 100, height: 100))
// 구조체 내부 변경과 함께 rect프로퍼티의 Property Observer가 감시하던 값을 출력한다. 
// (0.0, 0.0, 0.0, 0.0) will change to (0.0, 0.0, 100.0, 100.0)
// (0.0, 0.0, 0.0, 0.0) will changed to (0.0, 0.0, 100.0, 100.0)
~~~
<br>
<br>

# @ Swift 기술 질문

### # 애플리케이션 Life Cycle

- **iOS Application's Life Cycle** (SceneDelegate 추가 전 기준)
  - **UIApplication 객체생성**  -> **@UIApplicationMain 어노테이션 식별** -> **AppDelegate 싱글톤 객체 생성** -> 이후 **Main Event Loop를 실행** + **AppDelegate의 상황에 따른 감지 및 작업처리**

- **Application의 상태 분류**
  - **Not Running** : 아직 실행 안됨
  - **Foreground** : 앱이 화면에 나타나 있는 상태
    - Inactive : 특정한 액션이 없는 상태
    - Active : 특정 액션이 진행 중인 상태
  - **Background** : 앱이 백그라운드로 이동한 채 살아있는 상태
  - **Suspended** : 앱이 백그라운드로 이동한 채 어떤 실행이 없는 상태 
- **AppDelegate Delegate Methods**
  - application(_: **didFinishLaunchingWithOptions**:) 
    - **앱이 처음 시작될 때 호출**되는 델리게이트 메서드
  - **applicationDidBecomeActive**(_ application: UIApplication)
    - F**oreground의 Active 상태가 될때 호출**되는 델리게이트 메서드
  - **applicationWillResignActive**(_ application: UIApplication) 
    - **Foreground의 Inactive상태가 될 때 호출**되는 델리게이트 메서드
  - **applicationDidEnterBackground**(_ application: UIApplication) 
    - **Foreground -> Background 진입 시 호출**되는 델리게이트 메서드
  - **applicationWillenterForeground**(_ application: UIApplication)
    - **Background -> Foreground 진입 예정 시 호출**되는 델리게이트 메서드
  - **applicationWillTerminate**(_ application: UIApplication)
    - **Application 종료 직전 호출**되는 델리게이트 메서드



<br><br>



### # 뷰 컨트롤러의 Life Cycle

- **ViewController의 라이프 사이클 순서** 
  - **init** -> **loadView** -> **viewDidLoad** -> **viewWillAppear** -> **viewDidAppear** ->**viewWillDisappear** -> **viewDidDisappear** -> viewWillUnload/viewDidUnload(iOS6 이후 Deprecated 된 메서드)

<br><br>

#### 1) init() 

- 스토리보드[init?(coder:)]나 nib(xib)[init(nibName:bindle:)]파일을 통해 뷰 컨트롤러를 초기화하고 
- **뷰를 만들 때 사용할 정보를 뷰컨트롤러에 전달하는 단계**입니다. 

#### 2) LoadView()

- **뷰를 실제로 생성 후 메모리에 로드하는 단계** 
- 만약 **스토리보드나 nib(xib)를 사용하지 않는다면 해당 메소드를 오버라이드해서 사용할 뷰를 직접 생성, 뷰계층을 구성**해야합니다. 

#### 3) viewDidLoad()

- **loadView()로 뷰가 메모리에 로드된 직후에 해당 메소드를 실행**합니다. 
- 보통 이때 뷰 or 뷰컨트롤러에 대한 추가적인 초기화 설정을 합니다. 

#### 4) viewWillAppear(_:)

- **view가 view계층에 추가되기 직전(실제 뷰가 보여지기 직전), 뷰 애니메이션이 설정되기 전에 실행**된다. 
- 뷰가 화면에 나타나기 전에 해당 viewWillAppear를 오버라이드해서 필요한 작업을 수행할 수 있다. viewWillAppear를 오버라이드 하기 전에는 반드시 부모클래스의 viewWillAppear를 호출하도록 정의해야 한다. 
  - ☆ 만약 어떤 뷰컨트롤러가 다른 뷰컨트롤러를 popover 방식으로 띄운 후, 해당 뷰컨트롤러가 사라질때는 예외적으로 popover를 실행한 뷰 컨트롤러의 viewDidAppear가 실행되지 않는다. 

#### 5) viewDidAppear(_:)

- **view가 view계층에 추가된 직후에 실행**됩니다. 
- 해당 메서드를 오버라이드 해서 나타나는 뷰에 대한 추가적인 설정을 할 수 있는데 이때 반드시 부모 클래스의 viewDidAppear를 호출하도록 정의해야 합니다. 

#### 6) viewWillDisappear(_:)

- **view가 view계층에서 제거되기 직전에 viewWillDisappear(_:)가 호출**됩니다. 
- view가 view계층에서 제거되기 직전 최초 반응가(first responder)상태를 내려놓거나, 뷰의 설정 등의 작업이 가능합니다. viewWillDisappear를 오버라이드할때는 반드시 부모 클래스의 viewWillDisappear를 호출해야 합니다. 

#### 7) viewDidDisappear(_:) 

- **view가 view계층에서 제거된 이후에 호출**됩니다. 
- viewDidAppear(_:)에서 뷰가 제거된 후의 작업을 할 수 있으며 이때 부모클래스의 viewDidDisapear를 호출해야 합니다. 

#### - didReceiveMemoryWarning()

- **앱 실행 간 시스템 메모리가 부족한 상황이 되면, 시스템은 뷰컨트롤러에 메모리가 모자라다는 메세지를 보내며 didReceiveMemoryWarning()메서드를 호출**합니다. 
- **iOS6 이전에는 메모리 부족에 따라 시스템이 임의적으로 뷰를 해제 -> iOS6 이후에는 시스템이 직접 관여하지 않게 되므로서 임의 해제에 사용하던 viewWillUnload / viewDidUnload는 deprecated**되었습니다.
  - 해당 문제의 처리를 **didReceiveMemoryWarning에서 설정**하게 되었음.

#### **8) ViewController의 해제**

- **뷰 컨트롤러의 참조가 0이 되면 deinit()을 통해 뷰컨트롤러가 가지고 있던 뷰와 관련 자원들을 해제**함으로서 **완전히 ViewController의 생명주기가 종료**하게 됩니다.



<br><br>



### # iOS 주요 클래스, Main Classes 

### NSObject

- **Objective-C 클래스 계층 구조의 Root Class**

~~~ swift
class NSObject
~~~



<br><br>

### # 라이브러리, Library

- **프로그램이 연결할 수 있는 패키징 된 객체 파일들의 모음**
- **라이브러리 종류**
  - **정적라이브러리**
  - **공유라이브러리**



<br><br>



### # 프레임워크, Frameworks

- 라이브러리는 **실행가능한 코드**일 뿐이지만 **+ 프레임크는 다른 리소스의 하위 디렉토리를 포함하는 번들**이다. 

#### ## 코코아 터치 프레임워크 

- **코코아 터치 프레임워크 (Cocoa Touch FrameWork) 는 iOS 애플리케이션 개발환경**이다.
- **macOS 애플리케이션 제작 & 기능구현에 필요한 프레임워크를 포함하는 최상위 계층의 프레임워크**이다. 
- **코코아 터치는 핵심 프레임워크인 UIKit, Foundation을 포함**한다. 
- **코코아 (Cocoa) 란 NSObject를 상속받는 모든 클래스 및 객체를 가리킬 때 사용하는 단어**이다. 
- 코코아 (Cocoa) 란 이름의 기원
  - **커피원산지에서 따온 Java언어에 대항해 어린아이도 할 수 있는 Java라는 의미로 코코아 Cocoa로 명명**했다. 

#### ## Foundation Framework

- **CocoaTouch FrameWork에 포함되어있는 프로그램의 중심을 담당하는 프레임워크**이다. 
- **기본적인 원시 데이터 타입 (String, Int, Double) 등이 Foundation에 포함**되어있다. 
- **Foundation 기본 기능 셋**
  - Number, Data, String
    - **원시 데이터 타입의 제공**
  - Collection 
    - **Array, Dictionary, Set 등의 컬렉션 타입 제공**
  - Date, Time
    - **날짜와 시간을 계산하거나 비교**
  - Unit, Measurement
    - **물리적 차원을 숫자로 표현, 단위의 변환**
  - Data Formatting
    - **숫자, 날짜, 측정값 등을 문자열로 서로 변환**하는 작업
  - Filter, Sorting 
    - **컬렉션의 요소를 검사, 정렬**하는 작업



#### ## UIKit Framework

- **CocoaTouch FrameWork에 포함되어있는 UIKit Framework**
- **iOS 애플리케이션의 사용자 인터페이스를 구현하고 이벤트를 관리하는 프레임워크**이다.
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

- **읽기, 쓰기에 따라 그때그때 계산한 값을 내놓는 프로퍼티**
- **get || get+set 으로 구성**된다.
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

- **값이 변화했을때 변화 전(didSet) or 변화 후(willSet)의 값을 처리할 수 있는 프로퍼티**
- **didSet(값 변동 시 이전 값(oldValue)을 통해 처리) || willSet(값 변동 시 변동된 값(newValue)을 통해 처리)을 사용**한다. 
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

- **Lazy 변수는** 초기화 후 **실제 사용되었을때 부터 실제 연산**이 된다. 
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
    }()
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

- ARC는 **Automatic Reference Counting의 약어**이다.
- **ARC는 컴파일 시점에 동작**하며 **코드를 빌드(컴파일) 할 때 각 객체의 RC(Reference Count)를 추척하여 0이 되는 시점**에 자동으로 release 코드를 넣어 **해제해주는 방식**을 말한다. 

<br><br>





### # 옵셔널이란 무엇인가요?

- **강타입 언어인 Swift는 타입 안정성을 중요시**한다. 그런 **Swift언어에서 값이 없을 수(nil) 있음을 표현하는 것이 옵셔널**이다. 
- **옵셔널은 모나드의 일종**이다. 
- 옵**셔널 변수는 끝에 ''?'' 키워드가 붙으며 이는 강제언래핑(!) or 옵셔널바인딩을 통해 옵셔널을 실제 있는 값으로 래핑**하여 **사용할 수 있다.** 

<br><br>



### # map, flatMap, compactMap의 차이점

- **Map** 
  - **Sequence 요소들을 지정한 작업으로 Mapping** 시킨다. -> 결과에 Optional 중첩이 생길 수 있다.  
  - map은 functor라고 한다. 
- **FlatMap**
  - **Mapping + filter { $0 != nil } + 시퀀스들을 합쳐서 반환**한다.
  - map + flatten의 속성이 더해진 함수
  - **2차원배열을 1차원배열 로 flatten하게 만들어 사용하고자 할때 사용**할 수 있다.
  - Non-nil 상태(Optional값이 아닌) 결과들을 갖는 배열을 리턴한다. 
  - flatMap은 모나드라고 한다.
- **CompactMap** 
  - **Mapping + fillter { $0 != nil } 후 결과를 반환**한다. (swift 4.1에서 추가)
  - **1차원 배열 시퀀스에 대한 반환 결과는 FlatMap과 CompactMap이 동일**하다. 
    - 1차원 배열에서 nil을 필터링하며 Mapping하고자 한다면 compactMap을 쓰면 된다. 



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
    - **Controllers에 제공되는 블라인드 소통 방법**
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
    - 상대적으로 **비대해지는 ViewController에 대한 유지보수의 문제점**

<br><br>

### # 순환참조란 무엇인가요?

- **데드락(DeadLock), 교착상태, 병목현상**이라고도 한다. 
- **힙에 참조된 객체가 서로가 헤제되기를 무한정으로 기다리며 병목현상이 일어나는 것**을 말함

#### - Closure Capturing

- **iOS개발 간 마주할 수 있는 대표적인 교착상태 예시**로는 **Closure Capturing**이 있음.

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

- **Instrument의 Leak 도구를 이용**해서 체크
- **deinit 내 로깅코드를 통해 체크**한다. 
- **Xcode Memory Graph를 이용해서 Live Object, Leaking Object 확인**



<br><br>



### # strong, weak, unowned 키워드의 의미와 차이

- **Strong** 

  - **기본적으로 default는 strong으로 지정**된다. 

  - **strong 키워드로 선언된 멤버는 할당되는 순간 AC(Reference Count)를 증가시키고 1로 시작**한다. 

  - **RC를 증가시켜 ARC 사용 간 메모리 해제를 피하고 객체를 안전하게 사용하고자 할 때 사용**한다. 

  - Ex) **A라는 메서드에 a라는 레퍼런스 객체를 생성 (1 + 1 == 2) -> A 메서드 내에서 사용하고 A메서드가 종료하더라도 (2 - 1 == 1) RC는 0이 되지 않아 이후 다른 곳에서도 nil로 해제되지않고 해당 객체의 사용이 가능**해진다. 

    - 다만 **Closure 내에서 strong self 멤버를 사용 시, Closure Capturing 등의 문제 상황이 발생할 수 있어 주의가 필요**하다. 

  - **strong 객체 A 사용 예시 ▼**

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

- **weak** 
  
  - **객체가 할당 될 때 RC를 증가시키지 않는다. 또한 weak 키워드는 Optional에만 적용이 된다. ARC에 의해 RC가 0이 되면 해당 메모리는 해제되고 nil**이 된다. 
  - **클로저 내 상호참조로 인한 Closure Capturing을 해결할 수 있는 방법 중 하나**이다. 
  - **비교적 Life Cycle이 짧은 경우에 사용**한다. 
  
- **Unowned**
  
  - **객체가 할당 될 때 RC를 증가시키지 않는다.** 그러나 **weak 멤버와 달리 Non-Optional로 선언**되어야 하며, **ARC에 의해 메모리 해제가 된 후에도 해당 메모리의 값을 있는것으로 인지**하며 이 **해당 멤버가 nil인데 접근할 경우 앱 크래시가 발생**할 수 있다. 
  - **해당 객체의 Life Cycle이 명확하다고 개발자에 의해 판단이 서는 경우 사용하는게 좋다.**
  - **Non-Optional로 선언되므로 옵셔널 바인딩 등의 과정을 거치지 않고 weak 키워드 멤버보다 간결한 코딩이 가능**해진다. 



#### # Weak, unowned의 용도와 차이점

- **weak은 해당 값이 nil일 수도 있어 nil일 경우 해당 내용을 실행하지 않음으로서 클로져 캡쳐링을 방지**한다. 
  - ARC 카운트가 0이 되면 nil로 바꿔주는 런타임 작업이 존재한다.
- **unowned는 해당 멤버가 반드시 존재한다고 가정, 만약 힙에 해당 멤버가 없으면 런타임 중 앱 크래시를 발생**시킴으로서 **클로져 캡쳐링을 방지**한다.

<br><br>

### # IBOutlet의 weak 사용 여부 문제

- **iOS6 버전 까지**는 **앱 실행 간 메모리 부족문제가 발생할때 시스템이 임의로 viewWillUnload, viewDidUnload 함수를 사용하여 뷰를 해제**했는데 이때 **@IBOutlet 멤버 등의 경우 weak 설정이 되지 않으면 시스템이 뷰를 해제, 사용하지 않는 뷰 요소가 ARC에 의해 해제되지않고 남아있게 되는 문제**가 있을 수 있었다.
- **iOS6 이후**부터는 **시스템이 뷰의 해제에 임의로 관여하지 않고 대신 개발자가 didReceiveMemoryWarning()에서 메모리 부족 상황의 작업을 처리할 수 있게 됨**으로서 **@IBOutlet의 별도 weak 설정이 필요없게 되었다.** 
- 그렇게 시스템이 메모리 부족 상황에 대한 임의적 뷰 메모리 해제에 관여하지 않게 됨으로서 뷰 해제에 시스템이 사용하던 viewWilllUnload / viewDidUnload는 필요없게 되었다. (deprecated)

<br><br>

### # Escaping Closure의 개념 

- **메서드로 부터 실행된 closure를 메서드의 LifeCycle내에서 끝내지 않고 closure 내부의 결과를 외부에 전달하고자 할 때 사용**할 수 있다.
  - **콜백함수 같은 효과**를 볼 수 있음
- 해당 **메서드의 호출이 끝난 이후에도 closure는 메모리 어딘가에 저장되어 있어야하는데 이때 상황에 따라 weak 멤버등의 사용이 필요할 수 있음을 고려**해야한다. 
- **@escaping이 명시되어있지 않은 경우 일반적으로 non-escaping closure**이며, **non-escaping closure는 메서드 실행의 종료 이전에 closure의 사용이 모두 완료됨을 보장한다.**
  - **Non-escaping closure의 경우 weak 없이도 안전하게 사용할 수 있다.** 

<br><br>



### # 1급 객체, 성립 조건

- **swift의 함수(Closure)는 1급객체**이다.
- **1급 객체의 성립조건**
  - 변수나 데이터에 할당 될 수 있어야 한다. 
  - 객체의 인자로 넘길 수 있어야 한다. 
  - 객체의 리턴값으로 리턴 될 수 있어야 한다. 



<br>



### # 제네릭 (Generics)

- **제네릭은 Swift에서 가장 강력한 기능 중 하나로 Swift 표준 라이브러리 대부분이 제네릭코드로 만들어졌다.**

  - **그 예로 Array, Dictionary 등의 타입은 제네릭 타입**이다. 

- **제네릭의 장점**

  - **제네릭을 사용하면 코드를 유연하게 작성**할 수 있고, **재사용 가능한 함수와 타입이 어떤 타입과 작업할 지에 대한 요구사항을 정의**할 수 있다.
  - **타입만 다르고 코드의 내용이 대부분 일치할때 제네릭 사용을 통해 코드의 재사용성**을 높힐 수 있다.
  - **제네릭 타입을 준수하지 않는 경우 컴파일타임에 에러를 체크 가능**하다.

  - **컴파일러가 타입캐스팅을 해주므로 개발자가 편**리하다. 
    - ex) **'Array<Int>()'** 등의 **선언을 하면 알아서 Int형의 배열로 컴파일러가 타입캐스팅** 해준다.

  - **추상적인 방법으로 코드를 작성**할 수 있다. 

<br>

### # as, as?, as! 의 차이

- **as**
  - **컴파일러가 타입의 성공을 보장하는 타입캐스팅 방법**
  - **컴파일 타임에 캐스팅 가능/불가능 여부를 확인 가능**하다.
- **as?** 
  - **타입 변환에 실패할 경우 nil을 리턴**한다. 
  - 컴파일 타임에 캐스팅 가능/불가능 여부를 확인 불가(Xcode IDE에선 가능)

- **as!**
  - **타입 변환에 실패할 경우 앱 크래시가 발생**한다. 
  - 컴파일 타임에 캐스팅 가능/불가능 여부를 확인 불가(Xcode IDE에선 가능)
- ☆ Xcode 등의 일부 IDE에서는 정적 코드검사를 통해 as, as?, as! 모두에 대한 warning을 제공한다. 

<br><br>



### # Swift에서의 Class - Struct의 차이

- **Class**
  - **참조 타입** (Reference Type)
  - **객체로 사용 시 메모리 영역에 저상되며 ARC 체계로 메모리 해제가 이루어진다.** 
    - **멀티스레딩, 클로저 내 참조 시 ClosureCapturing 등의 메모리 순환에 주의**해야 한다.
  - **공짜 이니셜라이저가 존재하지 않는다.** 
  - **상속, 프로토콜 채택이 둘 다 가능하다.** 
  - **let으로 Class 객체 생성을 했어도 객체를 접근해서 객체 내의 variable 멤버의 값을 변경 가능**하다.
  - **Struct에서 멤버 값의 변화가 있을 수 있는 메서드에 사용하는 mutating 키워드를 사용할 필요가 없다.** 
- **Struct**
  - **값 타입** (Value Type)
  - **Struct는 대입 연산 시 값 자체가 복사되어 할당되며 원본과 공유가 불가능**하다. 
  - **불변성(Immutable) 구현에 유리**
  - **멀티스레딩에 안전**하다.
  - **공짜 이니셜라이저(자동 생성자)가 존재**한다. 
  - **상속이 불가능, 프로토콜 채택만 가능**하다. 
  - **let으로 Struct 객체를 생성하면 객체 내의 멤버가 variable이어도 해당 멤버의 값을 변경시킬 수 없다.** 
  - **객체 내의 멤버 변경을 요구하는 경우 mutating 키워드를 사용해서 메서드를 정의**한다. 



<br><br>

### # 익스텐션 Extension

- **익스텐션 (Extension) 은 iOS에서 매우 강력한 도구**이다.
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
- **Swift 내 문자열, 배열 등 많은 것들이 프로토콜을 사용**하고 있으며, **이들의 기초**가 되고 있다.
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

- **Equatable** 
  - **동일성 (Equality)를 비교할 수 있도록 하는 프로토콜**
  - **Equatable을 채택한 타입은 ==, != 등의 연산을 사용가능** 하다.
  - **Comparable, Hashable의 기반 프로토콜**이기도 하다. 
- **Comparable**
  - **Comparable 프로토콜은 표현하는 값이 순서를 가지고 있을 때 사용할 수 있는 프로토콜**이다.
  - **해당 프로토콜을 채택하면 >, >=, <, <= 의 부등호 비교 연산이 가능**해진다. 
  - **sequence, collection 등에서 정렬 등의 기능을 사용가능** 하다. 

- **Hashable**

  - Hasher를 통해서 **Int타입의 해쉬 값을 만들어 낼 수 있도록 만들어주는 프로토콜**
  - **Dictionary의 KeyType은 Hashable 프로토콜을 준수하는 값만 사용 가능**하다. 
  - **Set 타입은 Hashable 프토토콜을 준수한 값만 사용 가능**하다. 
  - **Hashable 프토토콜을 준수하기 위해서는 ==연산자, hashValue프로퍼티를 제공해야 한다.** 

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

<br><br>

### # 열거형 Enum

- Class, Struct와 더불어 **Swift 데이터 구조 중 하나인 Enum**
- Struct와 동일한 **값 타입의 데이터 타입**
- **메서드, 변수 등을 가질 수 있지만 enum 내 연동자료들을 제외하고는 별도의 저장공간을 갖고 있지 않다.**
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

- **Frame**
  - **SuperView(상위뷰) 좌표 시스템 내에서의 View 위치(origin)와 크기(size) 를 지정할 수 있다.**
  - **부모뷰의 기준에서 서브뷰의 위치와 크키를 지정**
- **Bounds**
  - **view 자기자신을 기준으로 한 좌표시스템에서의 위치(origin)와 크기(size)**
    - 기본적인 default origin은 x:0, y:0을 가리킨다. 
  - **부모 뷰의 위치관계와는 아무런 관계가 없다.** 
  - **특정 뷰의 bounds 값이 변경되면 해당 뷰의 서브뷰들의 드로잉 위치가 bound 값에 따라 변경 됨을 의미**한다. 
  - **bounds값이 변경될 때 subView의 위치가 바뀌는 것은 subView의 frame값이 변경된 것이 아니다.** 
    - **bounds값이 바뀌면서 해당 뷰의 좌표축이 변경되었기 때문**에 그에따라 **서브뷰의 드로잉 위치가 변경되는 것일 뿐이다.** 
  - **Bounds 실 사용 예시**
    - **UIScrollView/UITableView 등을 스크롤 할때 scrollView.bounds가 변경됨으로서 subView들의 위치가 달라지는 것인 bounds 특징의 예**이다. 
    - 이때도 **subView들의 frame은 변동되지 않는다.** 
      - **UIScrollView/UITableView 등의 bounds 값이 변경된 것**이다.



<br><br>

### # UIViewController 프로퍼티인 TopLayoutGuide, BottomLayoutGuide가 iOS11에서 deprecated된 이유와 대체수단

- 아이폰X가 생기면서 **iOS11 이후 안전영역에 대한 SafeAreaLayoutGuide가 생겼기 때문**이다.
  - **SafeAreaLayoutGuide**는 기존 Top, Bottom LayoutGuide와 **다르게 안전한 컨텐츠 영역의 개념**으로 등장했다.
- 기존 **TopLayoutGuide, BottomLayoutGuide는 두개의 사각 영역으로 되어있는 GuideArea였던 반면, SafeAreaLayoutGuide는 좌/우/위/아래의 하나의 사각 영역**으로 되어 있다. 



<br><br>



### # Timer 

- **일정 주기마다 특정한 작업을 처리하기 위해 사용**할 수 있음
- **scheduledTimer(withTimeInterval:, repeats:) { timer in ... }** 
  - **일정 주기별로 작업을 실행할 때 사용**한다. 
- **런루프에 등록이 되어 실행되며, invalidate 될 경우 nil이 되며 해제**된다. 
- 만약 **타이머가 nil인데 fire()함수로 타이머를 사용하려고 하면 앱크래시가 발생할 수 있다.** 
  - 그러므로 **이런 부분의 안정성을 확보하기 위해 weak키워드를 사용하는 것이 좋다.** 





<br><br>

### # UIStackView의 장점 

- **복잡한 제약 설정 없이 비교적 간단하게 복잡한 뷰 구조를 구현**할 수 있다. 
- **arrangedSubview로 UIStackView의 subView들이 관리**되며 하위뷰를은 UIStackView의 **alignment(세로방향), distribution(가로방향), Axis(가로/세로 기준), spacing(subView 간 간격)**의 **규칙에 의해 위치가 지정**된다. 



<br><br>



### # AutoLayout Constraint, Priority의 개념

- 이름 그대로 **AutoLayout 간 제약, 우선순위값을 의미한**다. 
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

- 일반적으로 변수가 특정 자료형으로 선언되지만 associatedtype을 통해 그 이외의 자료형으로 동적으로 타입이 변할 수 없다. 
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

<br><br>

### ## Functor, Monad

- **map을 적용할 수 있는 것은 Functor**이다.
- **flatMap을 적용할 수 있는 것은 Monad**이다.



<br><br>



### ## self vs Self

- **self**

  - **타입 인스턴스에서 자기자신을 가리키는 프로퍼티**
    - 해당 타입이 값타입이면 값타입처럼, 참조타입이면 클래스 인스턴스의 주소를 가지게 된다.

- **Self** 

  - **Self 또한 타입을 의미하지만 self와 용도의 차이**가 있다. 
  - 1) **Protocol 내부** 
    - **해당 프로토콜을 채택한 타입을 의미**
  - 2) **class 내부**
    - **해당 클래스의 타입 자체를 의미**한다. 

  ~~~ swift
  class A {
    	// 인스턴스 타입 A 자체를 반환
  		func someFunc() -> Self {
  				return self
  		}
  }
  ~~~

  - **그 외 구조체, 열거형에서는 Self를 사용할 수 없다.**

<br><br>

### # 예약어 문법

- **Defer**

  - **해당 블럭을 벗어날 때 실행할 작업을 블록  내에서 앞서 지정**할 수 있다. 

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



# @ CS 기술 질문



## # 알고리즘

## ## 자료구조

### **연결리스트 (Linked List)**

- **선형적으로 단방향으로 연결된 값의 컬렉션**
- **연결리스트 각각의 노드는 값과 next Node의 포인터를 갖고 있다.** 
- **Head Node 추가를 제외한 일반적인 경우 노드 추가, 삭제 시간복잡도는 O(N)으로 비효율** 적인 편인 자료구조
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
- **모든 노드가  leftChild, rightChild를 갖는 트리를 Full  Binary Tree** 라고 한다. 
- **Full Binary Tree 상태 + 최하위 노드가 몇개 비어있는 경우에는 작은 의미까지 포함할 경우 Complete Binary Tree**라고 하며, **Heap 자료구조로서 활용**될 수 있다.
- **InOrder** 
  - **트리를 최 좌측 -> 우측 순으로 차례대로 출력**하는 순서 방식 
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

## ## Sorting Methods, 정렬 방법

- **안정정렬/불안정정렬의 차이** : **같은 값이 존재할때 해당 값들의 인덱스 순서가 정렬 후에 유지될 수 있는지 여부에 따라 결정**된다. 

- **퀵 정렬 (Quick Sort)**
  - **평균적으로 단일 정렬기법 중 가장 좋은 성능을 보이는 정렬방법**, **피벗을 기준으로 피벗보다 작은값, 큰값을 비교하며 재귀, 분할정복방식으로 정렬을 수행**한다. 
  - **파티션, 분할정복을 활용**한다. 
    - **한번 파티션이 진행될 때마다 피벗을 기준으로 좌 우는 각각 피벗보다 작고(좌측) 피벗보다 큰(우측) 값으로 나뉘어 진다. 파티션이 된 후 양쪽에서 재귀적으로 분할정복방식으로 정렬**이 이루어진다.
  - **같은 값의 인덱스 위치가 바뀔 수 있는 불안정 정렬**
  - **최적의 상황에서 복잡도는 O(NlogN)** 이다.
    - 분할정복 알고리즘이 적용되어 정렬 체크구간이 쪼개질 수록 복잡도가 줄어든다.
  - **최악의 상황에서 복잡도는 O(N^2)** 이다.
    - **이미 정렬이 되어있는 상태에서 피벗이 양 끝에 위치할 경우 N^2번을 순회하며 분할정복의 이점을 활용하지 못하기 때문**이다. 
~~~ swift
import Foundation

func quickSort(_ arr: inout [Int], _ start: Int, _ end: Int) {
    if start >= end { return }
    let key = start
    var left = start + 1
    var right = end
    var temp = 0
    while left <= right {
        while left <= end && arr[key] >= arr[left] {
            left += 1
        }
        
        while right > start && arr[key] <= arr[right] {
            right -= 1
        }
        
        if left > right {
            temp = arr[right]
            arr[right] = arr[key]
            arr[key] = temp
        } else {
            temp = arr[right]
            arr[right] = arr[left]
            arr[left] = temp
        }
    } 
    
    quickSort(&arr, start, right-1)
    quickSort(&arr, right+1, end)
}

var arr = [3,1,5,4,2,6,9,7,8,0]
quickSort(&arr, 0, arr.count-1)
print(arr)

~~~

<br>

- **병합 정렬 (Merge Sort)**
  - **전체 배열집합을 하나의 단위로 분할 한 뒤 분할한 원소를 다시 병합하는 정렬** 방식
  - **퀵정렬과 함께 분할정복 정렬 알고리즘 기법 중 하나**
  - 불안정 정렬인 퀵정렬과 달리 **안정 정렬**
- **계수정렬 (Counting Sort)**
  - 계수가능 범위에서 배열 인덱스를 이용해 요소를 정렬한다. 
  - **복잡도는 O(N)로 매우 효율적**이다.
  - **일정 이상의 계수범위를 넘어갈 시 메모리의 과부하가 발생**할 수 있다. 
    - **매우 큰 계수 범위에 대한 사용 제한**
- **힙 정렬 (Heap Sort)** 
  - **Complete Binary Tree를 이용한 Heap 정렬**
  - **루트노드는 항상 최대 or 최솟값(특정 조건 하 Top 값)을 가진다.**
    - **이후 루트의 값을 마지막 자식노드와 바꾼 뒤 하위 노드와 크기를 비교하며 재정렬**을 하며 이를 **N번 반복하여 전체 정렬을 달성**한다. 
  - **불안정 정렬**
  - **일반 적인 복잡도는 어떤 정렬조건에서든 안정적인 O(NlogN)이다.**
- **삽입 정렬 (Insert Sort)**
  - 좌측부터해서 각 요소가 들어갈 위치를 현재까지 거쳐간 영역에 한해 순회탐색하여 비교하고 적절한 위치에 넣어준다. 
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

### ### C++ 언어

- **대표적인 객체지향 프로그래밍 언어** 
- **C++ 언어의 특징**
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
- **C++은 정적바인딩 (Static Dispatch)을 원칙**으로 작동한다.
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
  - **웹서버에서 지원되는 메소드 종류를 확인**한다.
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

- **TCP** (Transmission Control Protocol)
  - **전송 제어 프로토콜 규약**
  - **연결형 서비스로 가상 회선 방식을 제공**
  - **3-way handshaking 과정을 통해 연결설정**, **4-way handshaking으로 해제**한다. 
    - **목적지 ~ 수신지를 확실히 하여 정확한 전송 보장**을 위해 3-way/4-way handshaking을 사용한다. 
  - **높은 신뢰성을 보장**한다. 
  - **절차가 복잡하여 UDP보다 느리다.**
  - **전이중(Full-Duplex), 점대점(Point to Point) 방식**
- **UDP** (User Datagram Protocol)
  - **사용자 데이터그램 프로토콜 규약**
    - **데이터를 데이터그램 단위로 처리**하는 규약
    - **데이터그램 : 독립적인 관계를 지니는 패킷**
  - **비연결형 서비스**
  - **서버 소켓은 연결만을 담당한다.** 
  - **서버 ~ 클라이언트는 1대1로 연결**된다. 
  - **전송 데이터의 크기가 무제한**이다.
  - **신뢰성을 보장할 수 없다.** 
  - **절차가 단순하여 TCP보다 빠르다.**

<br><br>



## # 데이터베이스



### ## DBMS

- **데이터베이스 관리 시스템** (Database Management System)
  - 다수의 사용자들이 **DB 내의 데이터를 접근할 수 있도록 해주는 SW도구의 집합**



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

- **트랜젝션**
  - **트랜잭션은 데이터베이스의 논리적 연산단위**이다.
  - 데이터베이스 내에서 한꺼번에 수행되어야 할 일련의 연산집합

- **NoSQL**
  - **Not Only SQL의 약자,** 기존의 RDBMS와 다른 형태의 데이터로 저장하는 기술
  - 트랜잭션을 지원하지 않는다.

- **DDL** (Data Definition Language)
  - **데이터 정의 언어**
  - 데이터베이스 스키마를 정의 or 조작하기 위해 사용한다. 
  - CREATE, ALTER, DROP, TRUNCATE 등이 있다. 
- **DML** (Data Manipulation Language)
  - **데이터 조작 언어**, 데이터를 조작하기 위해 사용한다. 
  - SELECT, INSERT, DELETE, UPDATE
- **DCL** (Data Control Language)
  - **데이터 제어언어**
  - 데이터의 보안, 무결성 등을 정의하는데 사용한다. 
  - COMMIT, ROLLBACK, GRANT, REVOKE
- **DQL** (Data Query Language)
  - **SELECT만을 따로 분리해서 쿼리로 표현**하는 언어
- **TCL** (transaction Control Language)
  - **트랜젝션 제어 언어**

<br><br>
