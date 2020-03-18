

# CS 질문 답변 기록 2

### 프로그래밍 기본 CS

- 트러블슈팅 (Trouble Shooting)
  - 시스템이나 장치 등에서 발생한 장애를 다양한 수법을 활용해서 찾아내는 것

- **프로그램**
  - **static 하게 설치되어있는 코드, 커맨드, 실행명령 등의 집합**

- **프로세스**
  - **메모리에서 실행중인 프로그램 객체 자체**
  - **자기 자신만의 주소공간을 갖으며 독립적**임 (Self-Contained)
- **스레드(Thread)** 
  - **프로세스 내 실행 흐름 자체**를 스레드라고 한다. 
  - **한 프로세스는 여러 스레드를 사용할 수 있다.**
  - 프로세스 내의 독립적인 순차흐름 or 제어를 의미
- 멀티스레드(Multi-Thread) 
  - 하나의 프로세스에서 여러개의 스레드가 병행적으로 처리되는 것을 의미 
- 멀티테스킹 
  - Multi-Tasking, 두 개 이상의 프로세스를 실행하여 일을 처리하는 것을 의미
- **동시성 프로그래밍** (Concurrent Programming)
  - **다수의 프로그램들이 단일 CPU 상에서 동시에 실행되는 것**으로 **실제로 동시에 실행되는 것은 아님**
  - **모든 프로그램이 동시에 수행되는것처럼 보이게 동작하는 방식**입니다. 

- **병렬프로그래밍**
  - **다수의 프로그램들이 다수 CPU 상에서 실행**되는 것, 
  - **실제 동시에 여러 프로그램이 동작**함
- **비동기프로그래밍**
  - DispatchQueue
    - FIFO순서로 작업을 처리한다. 
    - Objective-C 위에서 작동합니다.
  - OperationQueue
    - FIFO순서로 작업을 처리하지만 조건에 따라 처리순서를 바꿀 수 있다. 
    - GCD에 비해 객체지향적으로 비동기 작업을 수행한다.
    - 보다 복잡한 비동기 작업(객체지향적인 작업)일 경우 DispatchQueue 대신 사용 할 수 있다.
    - 

- **http 프로토콜**
  - HTTP는 HyperText Transfer Protocol의 약어로 인터넷 상에서 데이터를 주고받기 위해 서버/클라이언트 모델을 따르는 프로토콜이다. 
  - 어플리케이션 레벨의 프로토콜로 TCP/IP 위에서 작동한다. 

- **링크드리스트 vs arrayList**
  - 링크드리스트 첫번째, 마지막 값 제거 O(1), 중간값 제거 O(N), 값 읽기 O(N)
  - 배열 첫번째 값 제거 O(N), 마지막 값 제거 O(1), 중간값 제거 O(1), 값 읽기 O(1)



- **CPU**
  - Central Processing Unit (중앙 처리 장치)
  - 컴퓨터 내 기억, 해석, 연산, 제어의 4대 기능을 담당하는 중앙처리 장치
  - 컴퓨터의 대뇌와 같다. 
- **RAM**
  - Random Access Memory
  - 컴퓨터 내 단기기억에 사용하는 단기기억 장치, 휘발성
- **ROM** 
  - Read Only Memory, 읽기 전용 기억장치, 비휘발성
- 하드디스크
  - 컴퓨터 장기기억에 사용하는 장기기억 장치

메모리에서 캐시의 역할, stack overflow와 buffer overflow의 차이

- **Stack OverFlow**
  - 프로그램이 자나치게 많은 버퍼 요청으로 현 운영체제에서 더이상 할당을 할 수 없게 될 때 발생하는 문제가 Stack OverFlow이다.
- **Buffer OverFlow**
  - 운영체제가 할당한 버퍼를 넘어선 영역에 프로그램이 접근할 경우 발생하는 문제가 Buffer OverFlow이다.



<br>

### Core Data

- **Core Data는 애플리케이션 내 모델 계층의 객체를 관리하기 위한 프레임워크**입니다. 해당 프레임워크는 **객체의 영속기능을 포함한 객체 생명주기 및 객체 관계도 관리 작업에 대한 일반적 / 자동화 된 방법을 제시**합니다. 
- **Core Data는 MVC 등 의 아키텍쳐 중 모델(Model)에서 사용하는 프레임워크** 라고 할 수 있습니다. 

<br>

### Core Animation

- **Core Animation은 시각적 요소 (visual elements)를 랜더링(합성), 애니메이션화 하는 것을 지원**합니다.
- **Core Animation은 CPU에 부담을 주지않고, 앱 속도 저하를 방지하면서도 높은 프레임, 부드러운 애니메이션을 구현 할 수 있도록 합니다.** 
  - 애니메이션 작업을 전용 그래픽 하드웨어에 넘겨 처리
- **Animation을 사용하는 방법은 크게 2가지**입니다. 
  - **UIView의 타입메서드, "animateWithDuration"을 사용하는 방법**
  - **Core Animation 을 사용하는 방법**

- 단순한 애니메이션이 아니라면 CoreAnimation을 사용하는 것이 좋다. 
- **Core Animation을 이해하기 위해서는 먼저 CALayer를 알아야 한다.** 

### CA 관련 NSObject 구성도 

- **NSObject** (objc 최상위계층 framework) 
  - - **CAAnimationGroup**
    - **CAPropertyAnimation**
      - **CABasicAnimation**
      - **CAKeyFrameAnimation**
    - **CATransition**

- Objective-C 최상위계층 프레임워크인 NSObject는 CAAnimation을 갖고 있습니다. 

- **CAAnimation을 상속 받는 3가지 객체**가 있다. 이 세 객체의 역할을 하나하나 보자면,

  - **CAAnimationGroup**
    - 다수 Animation을 묶어 동시에 수행하도록 해주는 객체입니다.
  - **CAPropertyAnimation**
    - **CA의 중심이 되는 것, CA에서 가장 많이 사용되는 것이 CAPropertyAnimation**이다.  
    - **CAPropertyAnimation은 추상클래스로서 CAPropertyAnimation을 상속받는 두 객체가  있다.** 
      - *CABasicAnimation*
      - *CAKeyFrameAnimation*

  - **CABasicAnimation**
    - **CABasicAnimation은 keypath를 이용해 property의 값을 변경하는 animation을 구현**할 수 있다. **property의 값을 설정하기 위해 fromValue, byValue, toValue 등을 사용**하게 되는데 이들의 **상관관계를 숙지해야 효과적인 animation을 구현**할 수 있다. 
    - **CABasicAnimation Property의 사용 예시**
      - fromValue, toValue 사용 : 해당 property가 fromValue -> toValue로 변한다. 
      - fromValue, byValue 사용 : 해당 property가 fromValue -> (fromValue + toValue)로 변한다.
      - byValue, toValue 사용 : 해당 property가 (toValue-byValue) -> toValue로 변한다. 
      - fromValue만 사용 : 해당 property가 fromValue -> animation 전 설정되었던 상태로 돌아간다.
      - toValue만 사용 : 해당 property가 animation 전 설정 상태 -> toValue로 변한다. 
      - byValue만 사용 : 해당 property가 animation 전 설정상태 -> (이전상태 + byValue)로 변한다. 
      - 아무것도 설정하지 않은 경우 : 해당 property의 직전 값 -> 현재 값으로 변한다. 
  - **CAKeyframeAnimation**
    - **CAKeyframeAnimation은 해당 property의 값을 연속적으로 바꾸는 animation을 사용하는 클래스**이다.
    - **property의 값 변화를 NSArray에 설정**한다.
    - **변화주기는 keyTime라는 property에 NSArray방식으로 설정**한다.  
      - 이때 **전체 변화주기(Overall Variation Period)는 0.0 ~ 1.0 범위로 분할 지정**한다. **이때 값을 부동소수점이어야 하며 순차적으로 이전 값보다 크거나 같은 값이 나와야 한다.**
    - **이후 전체 animation의 duration을 설정**하면 된다. 

- **CATransition**

  - **CATransition은 이미지의 전환을 필요로하는 animation을 지원하는 클래스**이다. 
  - **duration을 설정한 후 animation을 실행**시킨다. 해당 **layer의 이미지에 변화를 주면 CATransition은 해당 이미지 변화에 맞는 animation을 제공**한다. 

#### CALayer

- **CALayer는 이미지 기반 컨텐츠를 관리하고 해당 컨텐츠에 대한 애니메이션을 수행할 수 있게 해주는 객체**입니다. 
- **CALayer에서 제공하는 기능**
  - displayIfNeeded()
  - borderWidth
  - borderColor

## CocoaTouch Frameworks

- 코코아 터치 프레임워크는 iOS 애플리케이션 개발 환경으로, 애플리케이션의 다양한 기능 구현에 필요한 여러 프레임워크 (MapKit, CoreLocation, UIKit, Foundation, CoreData) 등을 포함하는 최상위 레벨 프레임워크입니다. 
- 코코아 프레임워크는 macOS 애플리케이션 제작에 사용하는 프레임워크입니다. 
- 코코아 터치는 핵심 프레임워크인 UIKit, Foundation을 포함합니다. 
- 코코아 라는 단어는 Objective-C 런타임을 기반으로 하며, NSObject를 상속받는 모든 클래스 & 객체를 가리킬 때 사용합니다. 

### Cocoa (Touch) 공식 문서 내용

- Cocoa, CocoaTouch는 OS X, iOS에서의 어플리케이션 개발 환경입니다. 
- Cocoa, CocoaTouch는 Objective-C 런타임과 2개의 핵심 프레임워크로 구성되어 있습니다. 
  - Cocoa는 Foundation, AppKit 프레임워크를 포함하며 OS X에서 동작하는 어플리케이션을 개발할때 사용됩니다. 
  - Cocoa Touch는 Foundation, UIKit 핵심프레임워크를 포함하며, iOS에서 동작하는 어플리케이션을 개발할 때 사용됩니다.
- **Note:**  용어, "Cocoa"는 일반적으로 Objective-C 최상단 root 클래스, NSObject를 상속하고, Objective-C 런타임을 기반으로 하고 있는 객체, 클래스를 의미해왔습니다. 
  - 이밖에도 "Cocoa" 혹은 "Cocoa Touch"는 OS X, iOS 플랫폼의 어플리케이션 개발 프로그래밍 인터페이스를 언급할때도 사용됩니다. 

#### The Frameworks

- 핵심프레임워크 중 하나인 Foundation 프레임워크는 기본적인 객체행위를 정의하고 있는 root 클래스, NSObject를 상속받고 있습니다. 
  - 이는 클래스들이 String, Number 등의 원시 데이터타입을 사용할 수 있게 해주며,
  -  Array, Dictionary, Set 등의 컬렉션도 사용할 수 있게 해줍니다.(데이터타입 및 컬렉션 대부분은 기본적으로 스위프트 표준 라이브러리에서도 제공하고 있습니다.)
- Foundation은 또한 국제화, 객체지속성, 파일관리, XML 처리 등을 위한 기능도 제공합니다. 
- 시스템 객체나 포트, 스레드, locks, 프로세스 등에 접근할 수 있습니다. 
- Foundation은 절차적 인터페이스를 표방하는 Core Foundation을 기반으로 합니다. (ANSI C)
  - ANSI : American National Standards Institute의 약자로 미국표준협회의 약자

당신은 애플리케이션의 유저 인터페이스 개발을 위해 AppKit, UIKit 프레임워크를 사용할 수 있습니다. AppKit, UIKit 프레임워크는 목적은 동일하나 플랫폼에 따라 다릅니다. 이 두개의 프레임워크는 이벤트처리, 그리기, 이미지처리, 텍스트처리, 응용프로그램 간 데이터 전송 등을 위한 클래스들을 포함하고 있습니다. 또한 TableView, Sliders, Buttons, TextFields, Alert 등의 다양한 유저-인터페이스 요소들을 포함합니다.

#### Objective-C

Objective-C는 Cocoa, CocoaTouch 어플리케이션 개발을 위한 기본 언어입니다. 하지만 Cocoa, CocoaTouch 어플리케이션은 C++, ANSI C 코드를 포함할 수도 있습니다. 추가적으로, Objective-C 런타임에 브릿지된 스크립트 언어인 PyObjC, RubyCocoa등을 사용하여 개발할 수도 있습니다. 

#### 관련 자료

- [Root class](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/RootClass.html#//apple_ref/doc/uid/TP40008195-CH46-SW1)
- [Objective-C](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/ObjectiveC.html#//apple_ref/doc/uid/TP40008195-CH43-SW1)

Cocoa (Touch) 관련 문서링크

https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/Cocoa.html



## UIKit

- **UIKit은 iOS 사용자 인터페이스를 구현, 이벤트를 처리하는 프레임워크**입니다. 
- UIKit 프레임워크 주요 역할
  -  **Gesture, Animation, Drawing, HandlingImage/Text 등 사용자 이벤트 처리를 위한 클래스를 포함**합니다. 
  - **테이블뷰, 슬라이더, 버튼 , 텍스트필드, Alert 창 등 애플리케이션의 화면을 구성하는 요소를 포함**합니다. 
- **사용자 인터페이스에 관련된 클래스는 애플리케이션의 Main Thread(or DispatchQueue.main... )에서만 사용해야 합니다.** 
  - ex) UI 관련 객체



### UITraitEnvironment

- **앱 내 iOS 인터페이스 환경을 구성하는 메서드의 집합**

- **Declaration**

~~~ swift 
protocol UITraitEnvironment
~~~

- **Overview**
  - iOS 인터페이스 환경은 수평, 수직 size 클래스, display 규모, 유저 인터페이스 관용구와 같은 특성(traits)를 포함합니다. UITraitEnvironment 프로토콜을 채택한 객체의 trait 환경에 접근하기 위해서 traitCollection property를 사용할 수 있습니다. 
  - 또한 UITraitEnvironment 프로토콜은 인터페이스 환경이 변경될 때 시스템이 호출하는 메서드도 제공하며 이들은 오버라이딩이 가능합니다. 이를 iOS app 환경에 맞게 활용할 수 있습니다. 
  - Trait collections에 대한 더 자세한 내용이 궁금하다면 UITraitCollection을 참조하세요. iOS 적응형 인터페이스 구축에 관한 WWDC 2014 presentation이 필요하다면 아래 링크를 참조하세요.

### IntrinsicContentSize

- UI의 본질적인 컨텐츠 사이즈

#### Declaration

~~~ swift
var intrinsicContentSize: CGSize { get }
~~~

#### Discussion

커스텀 뷰들은 전형적으로 화면에 나타날 때 레이아웃 시스템 상에서는 알수 없는 각자의 Content Size를 갖고 있습니다. 이때 프로퍼티를 설정하면 Content에 기반해서 어떤 크기가 되어야 할지에 대해 레이아웃 시스템과 소통할 수 있습니다. 

Intrinsic size는 컨텐츠 프레임에 대해 독립적이어야만 하는데 이는 레이아웃 시스템이 변경된 높이에 기반한 너비에 대해 동적으로 소통할 방법이 없기 때문입니다. 

만약 커스텀 뷰가 주어진 크기에 대한 본질적 크기가 없다면, 치수에 대하여 타입프로퍼티, noIntrinsicMetric(https://developer.apple.com/documentation/uikit/uiview/1622486-nointrinsicmetric) 이 사용될 수 있습니다. 

<br>

## Foundation

- **Foundation 프레임워크는 UIKit과 함께 코코아 터치 프레임워크에 포함된 핵심 프레임워크**입니다. 
- **Foundation은 원시 데이터 타입(String, Int, Double), 컬렉션 타입(Array, Dictionary, Set) 및 운영체제 서비스를 사용해 애플리케이션의 기본적인 기능을 관리하는 프레임워크**입니다. 
  - **실제 swift 에서는 데이터타입과 기능 대부분은 swift 표준 라이브러리에서 제공**합니다. 
- **Foundation 주요 역할**
  - Data타입 사용을 가능하게 해준다, array의 contains를 통한 문자열 검색(NSString 연동)을 가능하게 해준다.
  - Number, Data, String 원시 데이터타입 사용
    - Int, String, Character, Double 등 swift 표준 라이브러리에서 제공
  - Collection : Array, Dictionary, Set 등의 컬렉션 타입 사용 
    - Array, Dictionary, Set 등 컬렉션 타입 swit 표준 라이브러리에서 제공
  - Data & Time : 날짜와 시간을 계산 혹은 비교하는 작업
  - Unit, Measurement : 단위변환, 측정
  - Data Formatting : 숫자, 날짜, 측정값 등의 변환
  - Filter, Sorting : 컬렉션 요소를 검사하거나 정렬하는 작업
    - swift 표준 라이브러리에서 제공
  - 그 외... 파일 및 데이터 관리, 네트워킹 등...

### NSObject

- Objective-C 클래스 최상위 계층의 root 클래스
- Objective-C 객체로서 행동하고, Objective-C Runtime을 활용하기 위해 기본적으로 상속하는 클래스가 NSObject이빈다. 
- 객체생성, 해제 등에 따른 메모리 관리, 메시지디스패치, KVC, KVO, Objective-C Runtime 활용 등을 위해 사용한다.

### Objective-C Runtime

- iOS앱 개발을 통해 KVO, KVC 등의 기능을 사용하기 위해서는 Objective-C Runtime을 사용해야한다. 런타임이 있다는 것은 즉, Objective-C가 동적 언어(dynamic language)라는 것이다. 정적인 언어(static language)들의 경우 컴파일/링 시점에서 이미 코드가 어떻게 실행될지에 대한 모든것이 결정된다. 반면, 런타임을 지닌 동적 언어는 이런 결정들을 실제 각 코드가 실행되는 순간까지 미룰 수 있는 특징을 갖고 있다. 이런 objective-C의 동적 특징 덕분에 실제 코드가 실행중인 Runtime 상황에서 objective-C Runtime에 의해 원하는 객체로 메시지를 전송(Message Dispatch)하고, 메서드를 변경하고, 감지하는 등의 유연한 동작이 가능해진다. 

#### NSObject 클래스를 상속받는 이유

- Objective-C 프로그래밍을 하다보면 NSObject클래스를 상속받아 사용하게 되는 것을 알 수 있다. NSObject는 objective-C 최상위 프레임워크로서 NSObject를 상속받음으로서 Objective-C Runtime의 동작을 위한 추가 정보들이 자동으로 모든 클래스에 포함되어 컴파일이 되는 것이다. 덕분에 우리가 객체를 생성할때 원하는 형태로 메모리에 객체가 생성 될 수 있다. 