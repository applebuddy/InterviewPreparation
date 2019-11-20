# 면접 질문 정리 

- 면접에 나올 수 있는 기초 질문에 대한 답변 정리
- by applebuddy



<br>

<br>



### #1 뷰 컨트롤러의 Life Cycle

- ViewController의 라이프 사이클 순서 
  - init -> loadView -> viewDidLoad -> viewWillAppear -> viewDidAppear ->viewWillDisappear -> viewDidDisappear -> viewDidUnload(Deprecated)

<br>

#### init() 

- 스토리보드[init?(coder:)]나 nib(xib)[init(nibName:bindle:)]파일을 통해 뷰 컨트롤러를 초기화하고뷰를 만들때 사용할 정보를 뷰컨트롤러에 전달하는 단계입니다. 

#### LoadView()

- **뷰를 실제로 생성 후 메모리에 로드**합니다. 만약 **스토리보드나 nib(xib)를 사용하지 않는다면 해당 메소드를 오버라이드에서 뷰를 생성, 뷰계층을 구성**해야합니다. 

#### viewDidLoad()

- loadView()로 뷰가 메모리에 로드된 직후에 해당 메소드를 호출합니다. 이때 뷰 or 뷰컨트롤러에 대한 추가적인 설정을 합니다. 

#### viewWillAppear(_:)

- view가 view계층에 추가되기 직전, 뷰 애니메이션이 설정되기 전에 호출된다. 뷰가 화면에 나타나기 전에 해당 viewWillAppear를 오버라이드해서 필요한 작업을 수행할 수 있다. viewWillAppear를 오버라이드 하기 전에는 반드시 부모클래스의 viewWillAppear를 호출하도록 정의해야 한다. 
  - ☆ 만약 어떤 뷰컨트롤러가 다른 뷰컨트롤러를 popover 방식으로 띄운 후, 해당 뷰컨트롤러가 사라질때는 예외적으로 popover를 실행한 뷰 컨트롤러의 viewDidAppear가 실행되지 않는다. 

#### viewDidAppear(_:)

- view가 view계층에 추가된 직후에 실행됩니다. 해당 메서드를 오버라이드 해서 나타나는 뷰에 대한 추가적인 설정을 할 수 있는데 이때 반드시 부모 클래스의 viewDidAppear를 호출하도록 정의해야 합니다. 

#### viewWillDisappear(_:)

- view가 view계층에서 제거되기 직전에 viewWillDisappear(_:)가 호출됩니다. view가 view계층에서 제거되기 직전 최초 반응가(first responder)상태를 내려놓거나, 뷰의 설정 등의 작업이 가능합니다. viewWillDisappear를 오버라이드할때는 반드시 부모 클래스의 viewWillDisappear를 호출해야 합니다. 

#### viewDidDisappear(_:) 

- view가 view계층에서 제거된 이후에 호출됩니다. viewDidAppear(_:)에서 뷰가 제거된 후의 작업을 할 수 있으며 이때 부모클래스의 viewDidDisapear를 호출해야 합니다. 

#### didReceiveMemoryWarning()

- 앱 실행 간 시스템 메모리가 부족한 상황이 되면, 시스템은 뷰컨트롤에 메모리가 모자라다는 메세지를 보내며 didReceiveMemoryWarning()메서드를 호출합니다. 
- iOS6 이전 메모리 부족에 따라 시스템이 임의적으로 뷰를 헤제하던 것에서 iOS6 이후에는 시스템이 직접 관여하지 않게 되므로서 임의 해제에 사용하던 viewWillUnload / viewDidUnload는 deprecated되었습니다.
  - 그걸 didReceiveMemoryWarning에서 처리하게 됨

뷰 컨트롤의 참조가 0이 되면 deinit()을 통해 뷰컨트롤러가 가지고 있던 뷰와 관련 자원들을 해제함으로서 완련히 ViewController의 생명주기가 끝나게 됩니다...