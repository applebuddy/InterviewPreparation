

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

### DataBase

- *간단한 데이터는 UserDefaults 객체를 이용해 프로퍼티 리스트(plist)에, 조금 더 복잡한 데이터는 커스텀 프로퍼티 리스트에 저장했다. 하지만, GPS 정보 기록 등 점차 누적되는 데이터, 배열 형태의 데이터를 저장하기에는 적합한 기술이 아니다.*
  - 프로퍼티 리스트는 데이터를 쌓기보다는 단건의 데이터를 갱신하는 데에 초점이 맞추어진 저장 기술이라고 보는 것이 맞기 때문이다. 
    - 프로퍼티 리스트는 iOS, macOS 등 애플 사이드에 국한된 개념입니다. 
  - 또한 배열타입으로 저장된 데이터는 범위를 지정해서 읽을 수 없고 모든것을 읽을때마다 한꺼번에 읽어들여야 한다는 단점이 있다. 비효율성도 이런 비효율성이 없을 것입니다. 만약 회사에서 복잡한 데이터를 plist에 저장한다면 코드 리뷰 때 선임에게 혼이 날 수도 있습니다.
- **이러한 프로퍼티 리스트를 대신해 데이터를 효율적으로 저장할 수 있는 대안이 데이터베이스**입니다. 데이터베이스는 **대량의 데이터를 구조적으로 관리하기 위해 만들어진 기술로 우리에게 필요한 데이터를 처리하기에 매우 적절**합니다. **필요한 범위의 데이터만 선택적으로 읽어들일 수 있으며, 신규 데이터를 추가하기 위해 매번 전체 데이터를 읽어오지 않아도 되는 것 역시 큰 장점**입니다. 이런 특성 덕에 **데이터베이스는 매우 고속으로 데이터를 처리할 수 있으며 메모리관리나 성능향상에도 큰 도움**을 줍니다. 

- 줄여서 DB라고도 부르는 데이터베이스는 여러 사람이 공유하고 사용 할 목적으로 통합하여 관리되는 데이터의 집합입니다.
- 데이터베이스론에 따르면 데이터베이스는 다음과 같은 특성을 지닙니다. ▼
  - **똑같은 자료를 중복 없이 통합적으로 저장**한다.
  - **컴퓨터가 접근하여 처리할 수 있는 저장장치에 기록**된다.
  - **어떤 조직의 기능을 수행하는 데 없어서는 안되는 필수요소로, 존재 목적이 뚜렷**하다.
  - 실시간으로 접근하여 데이터를 읽거나 쓸 수 있다. 
  - 데이터베이스에 저장된 데이터는 추가, 수정, 삭제 등 지속적으로 변한다.

### Core Data

- Cocoa 전용의 데이터 프레임워크로 CoreData는 애플이 코코아 개발환경을 통해 제공하는 인메모리(In-Memory) 방식의 데이터 관리 프레임워크입니다. **우리는 코어 데이터를 사용하여 예의 데이터베이스 개발 환경과 유사하게 데이터를 읽고 쓰며 수정하고 삭제할 수 있습니다.** 코어 데이터는 **iOS 및 macOS 환경을 지원**하며, **objective-C와 스위프트 언어 역시 모두 지원**합니다. 
- **CoreData는 인메모리 방식인 만큼, 코어 데이터에서 데이터를 다루는 모두 작업은 메모리를 기반으로 동작**합니다. 다시말해, 코어 데이터를 통해 읽고 쓰는 모든 데이터는 원칙적으로 메모리에 로드된 후 처리됩니다. 덕분에 대량의 읽기, 쓰기 작업이 발생하더라도 성능에 크게 영향을 끼치지 않습니다. 이는 대부분의 작업이 영구 저장소에서 직접 처리되고, 효율성을 위해 읽기 목적의 데이터 일부만 메모리에 올려놓고 사용하는 데이터베이스와는 구분되는 효율적 특성입니다. 
- **CoreData가 인메모리 기반이라 하더라도 코어 데이터 내부적으로는 파일이나 SQLite 같은 영구 저장소에 보조적으로 데이터를 저장할 수 있기 떄문에, 앱이 종료되더라도 데이터가 삭제되지는 않습니다.** 
- **CoreData가 사용하는 데이터 저장 구조는 SQLite의 그것과 상당히 유사**합니다. 데이터베이스 파일에 해당하는 데이터 모델 파일이 있고, 테이블을 통해 데이터 저장구조를 정의하는 것과 유사하게 코어 데이터에서는 엔티티(Entitiy)를 통해 데이터 저장 구조를 정의합니다. 테이블의 하위 구조인 칼럼은 엔티티의 하위구조인 attribute와 개념적으로 대응되며, 정규화된 데이터를 읽어오기 위해 사용하는 왜래 키 및 조인은 엔티티의 하위 구조를 이루는 또 다른 한 축인 릴레이션으로 대응됩니다. 

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

<br>

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

#### AppKit

AppKit은 macOS상에서 그래픽적인, 이벤트기반의 유저인터페이스를 관리하고 구축해주는 역할을 한다. 

#### 관련 자료

- [Root class](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/RootClass.html#//apple_ref/doc/uid/TP40008195-CH46-SW1)
- [Objective-C](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/ObjectiveC.html#//apple_ref/doc/uid/TP40008195-CH43-SW1)

Cocoa (Touch) 관련 문서링크

https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/Cocoa.html

<br>

## UIKit

- **UIKit은 iOS 사용자 인터페이스를 구현, 이벤트를 처리하는 프레임워크**입니다. 
- UIKit 프레임워크 주요 역할
  -  **Gesture, Animation, Drawing, HandlingImage/Text 등 사용자 이벤트 처리를 위한 클래스를 포함**합니다. 
  - **테이블뷰, 슬라이더, 버튼 , 텍스트필드, Alert 창 등 애플리케이션의 화면을 구성하는 요소를 포함**합니다. 
- **사용자 인터페이스에 관련된 클래스는 애플리케이션의 Main Thread(or DispatchQueue.main... )에서만 사용해야 합니다.** 
  - ex) UI 관련 객체

<br>

### UIResponder

이벤트를 처리하고 반응하기 위한 추상 인터페이스 (abstract interface)

#### Declaration

class UIResponder: NSObject // UIResponder는 NSObject를 상속받는다. 

#### Overview

UIResponder의 인스턴스들, Responder 객체들은 UIKit app의 이벤트 처리관련 뼈대를 구성합니다. 

그 예로 UIApplication, UIViewController, 모든 UIView 객체들 (UIWindow를 포함하는)을 포함합니다. 

이벤트가 발생했을 때, UIKit에서는 처리를 위해 이벤트를 Responder 객체들로 전송합니다. 이때의 이벤트종류로는 터치이벤트, 모션이벤트, 원경제어이벤트, 압력이벤트 등이 있습니다. 구체적인 타입의 이벤트를 다루기 위해 Responder는 이에 맞는 메서드들을 오버라이딩해야합니다. 그 예로, 터치이벤트를 다루기 위해서는 Responder는 touchesBegan(_:with:), touchesMoved(_:with:), touchesEnded(_:with:), touchesCancelled(_:with:) 메서드를 사용합니다. 터치의 경우, Responder는 앱의 인터페이스를 적절하게 업데이트하고, 터치의 트랙을 추적하기 위해 UIKit에서 제공되는 이벤트 정보를 사용합니다. 

https://developer.apple.com/documentation/uikit/uiresponder/1621142-touchesbegan

https://developer.apple.com/documentation/uikit/uiresponder/1621107-touchesmoved

https://developer.apple.com/documentation/uikit/uiresponder/1621084-touchesended

https://developer.apple.com/documentation/uikit/uiresponder/1621116-touchescancelled

처리 이벤트 (Handling Events) 뿐만 아니라, UIKit Responder는 App의 처리되지 않은 이벤트를 앱의 다른 파트로 전송하는 것을 관리해줍니다. 만약 주어진 Responder가 이벤트를 처리하지 앟는다면, 해당 이벤트를 Responder Chain의 다음 이벤트로 전달합니다. UIKit은 사전에 정의된 규칙을 사용해 어떤 객체가 다음 이벤트를 수신해야할 지 결정하며 Responder Chain을 동적으로 관리합니다. 예를들어 뷰가 자신의 수퍼뷰에게 이벤트를 전달하고, 계층 구조의 root뷰는 이를 뷰컨트롤러로 전달합니다. 

UIView -> UIView's superView -> UIViewController -> UIWindow -> UIApplication -> UIApplicationDelegate

Responder들은 UIEvent 객체들을 처리하지만, 또한 입력 뷰를 통한 커스텀 입력을 받을 수도 있습니다. 시스템의 키보드가 대표적인 예라고 할 수 있겠습니다. 유저가 스크린상의 UITextField, UITextView 객체를 텝했을 때, View는 first Responder가 되며 자신의 input View, system keyboard를 보여줍니다. 유사하게, 당신은 커스텀 input View를 만들고 다른 Responder들이 활성화 되었을때 이를 보여줄 수 있습니다. 커스텀 input View를 Responder와 연관짓기 위해서는 해당 뷰를 Responder의 input View에 할당하세요. Responder와 Responder Chain 관련 정보를 얻고 싶으시다면, Event Handling Guide for UIKit Apps 를 참조하세요.



https://developer.apple.com/documentation/uikit/#//apple_ref/doc/uid/TP40009541



<br>

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

<br>

### NSObject

- Objective-C 클래스 최상위 계층의 root 클래스
- Objective-C 객체로서 행동하고, Objective-C Runtime을 활용하기 위해 기본적으로 상속하는 클래스가 NSObject이빈다. 
- 객체생성, 해제 등에 따른 메모리 관리, 메시지디스패치, KVC, KVO, Objective-C Runtime 활용 등을 위해 사용한다.

<br>

### Objective-C Runtime

- iOS앱 개발을 통해 KVO, KVC 등의 기능을 사용하기 위해서는 Objective-C Runtime을 사용해야한다. 런타임이 있다는 것은 즉, Objective-C가 동적 언어(dynamic language)라는 것이다. 정적인 언어(static language)들의 경우 컴파일/링 시점에서 이미 코드가 어떻게 실행될지에 대한 모든것이 결정된다. 반면, 런타임을 지닌 동적 언어는 이런 결정들을 실제 각 코드가 실행되는 순간까지 미룰 수 있는 특징을 갖고 있다. 이런 objective-C의 동적 특징 덕분에 실제 코드가 실행중인 Runtime 상황에서 objective-C Runtime에 의해 원하는 객체로 메시지를 전송(Message Dispatch)하고, 메서드를 변경하고, 감지하는 등의 유연한 동작이 가능해진다. 

#### NSObject 클래스를 상속받는 이유

- Objective-C 프로그래밍을 하다보면 NSObject클래스를 상속받아 사용하게 되는 것을 알 수 있다. NSObject는 objective-C 최상위 프레임워크로서 NSObject를 상속받음으로서 Objective-C Runtime의 동작을 위한 추가 정보들이 자동으로 모든 클래스에 포함되어 컴파일이 되는 것이다. 덕분에 우리가 객체를 생성할때 원하는 형태로 메모리에 객체가 생성 될 수 있다. 