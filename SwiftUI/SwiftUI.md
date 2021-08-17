# SwiftUI

- Swift 언어 기반의 UI 프레임워크

<br />

### SwiftUI의 4가지 원칙

- 선언형

   - 명령형 : 어떻게 동작해야 하는지에 초점, 프로그램의 상태를 변화시키는 구문들에 초점

   - 선언형 : 무엇을 하는지에 초점, 어떻게 흘러가는지에 대한 묘사 없이 오직 프로그램의 논리에 초점

- 자동화

   - 가능한 많은 기능이 자동으로 수행될 수 있게 제공

   - 매번 직접 작성해 주어야 했던 많은 상용구를 생략할 수 있다

- 조합

   - 뷰의 조합과 분리를 간단히 할 수 있게 제공

   - 큰 뷰를 하나의 기능을 가진 작은 뷰들로 잘게 나누거나 각각의 뷰를 조합해 원하는 뷰를 쉽게 만들 수 있게 지원

- 일관성

   - UI는 항상 데이터와 동기화되어 일관성 있게 보여야 한다는 점

   - 뷰의 특정 상태를 저장할 State나 모델 객체의 변화를 관찰할 ObsevableObject 같은 원천 자료(Source Of Truth)의 변화를 반영해 뷰에 반영

<br />

#### SwiftUI vs Storyboard

- ContentView.swift

   - swiftUI는 뷰 프로토콜을 준수하는 구조체를 사용해 body 프로퍼티에 UI를 구성하는 코드를 작성한다 따라서 ContentView가 View Controller를 대체

- Main.storyboard 삭제

- Preview Assets.xcassets 추가

   - 개발 과정에서 프리뷰만을 위한 별도의 에셋 파일을 관리하는 기능 제공

   <br />

<br />

#### Content View

- 뷰 프로토콜

   - View 타입은 기존의 UIView와 달리 프로토콜로 선언

   - 필수로 구현해 주어야 하는 것은 읽기 전용인 body 연산 프로퍼티 뿐

   - 기존의 UIView 클래스가 상당히 많은 수의 프로퍼티를 가지는 것과 대조적

      - UIView는 사용 목적과 관계 없이 모든 프로퍼티를 보유해야 한다는 단점

      - 그래서 SwiftUI에서는 각각의 뷰 객체가 자신에게 필요한 속성만 가지고 필요한 뷰를 생성하도록 구현

   - body 프로퍼티의 반환 타입이 또다시 뷰 프로토콜을 준수

      - 무한재귀?

      - 실제 콘텐츠를 표현하는 기본 뷰와 컨테이너 뷰는 재귀호출이 일어나지 않게 Never 타입 사용

         - typealias Body = Never

#### 수식어(Modifier)

- 뷰에서 사용 가능한 메서드

- 추가 동작이나 시각적 변화가 가미된 새로운 뷰를 반환하는 메서드

- 뷰가 다시 또 다른 뷰를 반환하게 하는 메서드

#### Life Cycle

- UIKit App Delegate

   - SceneDelegate.swift 에서 앱의 Life Cycle을 관리

   - UIHostingController : UIViewController를 상속 받고, 뷰 프로토콜을 준수하는 제네릭 매개 변수 Content를 전달 받는 제네릭 클래스

- SwiftUI App

   - SceneDelegate.swift 대신 프로젝트명.swift가 존재

   - SceneDelegate에서 담당했던 Life Cycle을 WindowGroup에 onChange 이벤트를 통해 감지

   - iOS 14 이상에서만 지원

#### AutoLayout

- SwiftUI에서는 더이상 사용하지 않는다

- 프레임워크 내부에선 활용되지만, 개발자가 직접 다뤄야 하는 일이 사라졌다는 의미

- SwiftUI가 제공하는 자동화의 일부에 포함

- 그 대신 박스형 레이아웃 시스템과 선언형 문법을 이용해 UI 요소들을 배치

<br />

| UIKit | SwiftUI |
 | --- | --- |
| UILabel | Text |
| UITextField | TextField |
| UITextField(isSecureTextEntry) | SecureField |
| UIButton | Button |
| UIImageView | Image |
| UISwifth | Toggle |
| UISlider | Slider |
| UIStepper | Stepper |
| UIPickerView | Picker(WheelPickerStyle) |
| UISegmentedControl | Picker(SegmentedPickerStyle) |
| UIDatePicker | DatePicker |
| UITextView | 동일 요소 없음 |
| UIStackView | HStack(가로 방향), ZStack(세로 방향) |
| UIScrollView | ScrollView |
| UITableView(Plain) | List |
| UITableView(Grouped) | List(GroupedListStyle) |
| UICollectionView | 동일 요소 없음 |

| UIKit | SwiftUI |
 | --- | --- |
| UIViewController | View |
| UINavigationController | NavigationView |
| UITabBarController | TabView |
| UISplitViewController | NavigationView |
| UITableViewController | List |
| UICollectionViewController | 동일 요소 없음 |
| UIAlertController(actionSheet) | ActionSheet |
| UIAlertController(alert) | Alert |

#### 텍스트(Text)

- 화면에 원하는 문자열을 표현하는 뷰

- 텍스트에 적용할 수 있는 수식어

   ```swift
   struct ContentView: View {
       var body: some View {
           VStack(spacing: 30) {
               Text("폰트와 굵기 설정")
                   .font(.title)       // 폰트 설정
                   .fontWeight(.black) // 폰트 굵기
               
               Text("글자색은 foreground, 배경은 background")
                   .foregroundColor(.white)    // 글자색
                   .padding()                  // 택스트 주변 여백 설정
                   .background(Color.blue)     // 텍스트 배경 설정(Color 명시)
               
               Text("커스텀 폰트, 볼드체, 이탤릭체, 밑줄, 취소선")
                   .font(.custom("Menlo", size: 16))
                   .bold()             // 볼드체
                   .italic()           // 이탤릭체
                   .underline()        // 밑줄
                   .strikethrough()    // 취소선
               
               Text("라인 수 제한과 \n 텍스트 정렬 기능입니다. \n 이건 안 보입니다.")
                   .lineLimit(2)                       // 텍스트 최대 2줄 표현
                   .multilineTextAlignment(.trailing)  // 다중행 문자열 정렬 방식 지정
                   .fixedSize()                        // 주어진 공간의 크기가 작아도 텍스트를 생략하지 않고 표현되도록 설정
               
               // 2개 이상의 텍스트를 하나로 묶어서 동시에 적용
               (Text("자간과 기준선").kerning(8)     // 자간
                   + Text(" 조정도 쉽게 가능합니다.").baselineOffset(8)) // 기준선
                   .font(.system(size: 16))
           }
       }
   }
   ```

   ![swiftui-image-0](./images/swiftui-image-0.png)

   <br />

#### 이미지(Image)

- UIKit의  UIImageView와 같이 지정된 이미지를 표현하는 뷰

- 이미지는 기본적으로 주어진 공간과 관계 없이 그 고유의 크기를 유지한다.
ex) 100 x 100 크기의 이미지를 200 x 200의 크기로 변경할 때 frame 수식어를 적용해도 이미지의 크기는 변하지 않고 뷰가 차지하는 공간만 달라진다.

- resizable : 이미지의 크기를 변경해야 하는 경우 resizable 수식어를 적용해야 한다.C

   | UIKit | SwiftUI | 설명 |
    | --- | --- | --- |
   | Scale To Fill | 기본값 | 비율과 관계 없이 이미지를 늘려서 주어진 공간을 가득 채움 |
   | Aspect Fit | .scaleToFit() | 이미지 원본의 비율을 그대로 유지한 상태에서, 가능한 최대 크기까지 늘어남, 최대 크기는 주어진 공간의 너비와 높이 중 작은 값을 기준 |
   | Aspect Fill | .scaledToFill() | 이미지 원본의 비율을 그대로 유지한 상태에서 가능한 최대 크기까지 늘어남, 최대 크기는 주어진 공간의 너비와 높이 중 큰 값을 기준, 이미지의 일부가 주어진 공간을 벗어나 더 크게 표현될 수 있음 |

- AspectRatio : 이미지 비율에 대해 세부적인 조정이 필요할 때 사용하는 수식어

   - 콘텐츠 모드가 반영된 상태에서 추가로 이미지의 너비와 높이의 비율 조정

- ClipShape : 이미지를 원하는 모양으로 만들 때 사용하는 수식어

- RenderingMode 

   - template : 이미지의 불투명 영역이 가진 본래의 색을 무시하고 원하는 색으로 변경해 템플릿 이미지로 활용

   - original : 항상 이미지 본래의 색을 유지

- ImageScale : 이미지의 크기 설정, small, medium, large

- Font : 이미지 스케일 이외에도 폰트를 이용해 크기 변경 가능

- Weight : 이미지에는 굵기를 바로 조정할 수 있는 수식어가 없어, 굵기를 변경하려면 font 수식어를 이용해서 변경

<br />

#### 뷰 레이아웃

- 스택

   - SwiftUI 내부에서 뷰를 배치하는 데 사용하는 컨테이너 뷰

   - 뷰 프로토콜을 준수하는 Content를 제네릭 매개 변수로 받아 자식 뷰로 표현하는 제네릭 구조체로 선언되어 있으며, 그 자신도 뷰 프로토콜을 채택

   - 스택을 사용하면 콘텐츠로 전달받은 자식 뷰들을 특정 방식으로 표현하는 하나의 새로운 뷰가 만들어짐 

   - Horizontal Stack(HStack) : 가로 방향으로 뷰 배열

   - Vertical Stack(VStack) : 세로 방향으로 뷰 배열

   - Depth Stack(ZStack) : 뷰 계층을 겹겹이 쌓아 올리는 형태로 배열

   - 생성자

      - alignment : 뷰의 정렬, 기본값 .center

      - spacing : 자식 뷰 간에 간격, 기본값 nil, nil 인 경우 뷰에 따라 다른 기본값 적용

      - content : 실제 콘텐츠

- Spacer 

   - 뷰 사이의 간격을 설정하거나 뷰의 크기를 확장할 용도로 사용되는 레이아웃을 위한 뷰

   - Spacer는 스택 외부에서 사용될 때와 스택 내부에서 사용될 때 그 특성이 각각 달라지게 된다.

   - 스택 외부에서 단독 사용될 경우 부모 뷰가 제공하는 공간 내에서 가능한 최대 크기로 확장하며, 시각적 요소를 적용할 수 있는 하나의 뷰로 사용

   - ZStack의 경우도 그 특성상 각각 개별적인 뷰가 게층 구조를 이루고 있는 것으로 취급되므로 스택 외부에서 사용된 Spacer와 동일하게 취급

   - HStack, VStack의 경우 시각적 요소가 제외되고 공간을 차지하기 위한 역할로만 기능, 콘텐츠 없이 단독 사용되는 경우 아예 뷰가 없는 것으로 취급

   - frame : 길이 제한 수식어

   - minLength : 최소 간격 지정

- Overlay

   - 뷰 원본의 공간을 기준으로 그 위에 새로운 뷰를 중첩하여 쌓는 기능을 하는 수식어

   - UIKit의 addSubview 메서드를 사용하는 개념과 유사

- Background

   - overlay와 마찬가지로 뷰 원본의 공간을 기준으로 뷰를 중첩하는 것은 같지만, 위가 아니라 아래 방향으로 쌓아 나간다.

   <br />

#### 불투명 타입

- 특정 실체 타입을 반환하는 대신, 타입 정보를 숨기고 프로토콜에 대한 정보만 남긴 채 API를 사용할 수 있도록 도와주는 타입

- 컴파일러만 정확한 타입 정보에 접근하고 모듈의 클라이언트는 불투명한 타입을 이용하도록 강제하는 역할

- 프레임워크나 라이브러리 제공자 측에서 구현에 사용하는 구체적인 타입들을 명시하는 대신, API를 추상화하고 모듈 간 결합성을 낮추는 데 도움

- 제네릭을 반대로 적용하는 것과 같은 개념이기 때문에 리버스 제네릭이라고도 함

   - 제네릭 : 코드를 호출하는 측(caller)에서 호출되는 측(callee)의 타입을 결정

      ```swift
      func genericFunction<T: Animal>(_ animal: T) { ... }
      genericFunction(Dog())
      genericFunction(Cat())
      ```

   - 불투명 타입 : 호출된 코드가 호출한 코드의 타입을 결정

      ```swift
      // 호출된 쪽에서 타입 결정
      func opaqueTypeFunction() -> some Animal { Dog() }
      // 호출한 측은 추상화된 타입을 전달
      let animal: some Anmial = opaqueTypeFunction()
      ```

      <br />

#### 버튼(Button)

- 유저가 탭을 하는 것처럼 지정 이벤트가 발생했을 때 특정 작업을 수행하게 하는 가장 기본적인 컨트롤

   - 뷰 : 화면에 콘텐츠를 표현하는 것에만 초점을 맞춘 것

   - 컨트롤 : 유저와의 상호작용을 할 수 있도록 추가적인 행동이 정의된 뷰

- UIButton 같은 역할

| 구분 | 설명 |
 | --- | --- |
| DefaultButtonStyle | buttonStyle 수식어 생략 시 기본 적용값, 모든 OS에서 공통으로 사용할 수 있는 버튼 스타일, 버튼이 사용된 환경에 따라 시스템이 알아서 적절한 버튼 스타일 반영 |
| BorderlessButtonStyle | iOS에서 대부분의 경우 기본 반영되는 스타일, 콘텐츠에 미리 지정된 시각적 효과가 적용되며 그 명칭이 의미하는 것처럼 테두리를 그리지 않는다. iOS에서 제공되는 버튼 스타일 중 테두리를 그리는 것은 없지만, macOS에선 BorderedButtonStyle이 함께 제공되므로 대조되는 의미에서 이 이름 사용, watchOS에선 사용할 수 없다. |
| PlainButtonStyle | 모든 OS에서 공통으로 사용할 수 있는 버튼 스타일, 유휴 상태(IDLE)에서는 버튼의 콘텐츠에 어떤 시각적 요소도 적용하지 않는다. |

<br />

#### onTapGesture

- onTapGesture를 사용해 버튼을 사용하지 않고도 같은 기능을 하게 구현 가능

<br />

<br />

### 내비게이션 뷰(NavigationView)

#### 내비게이션 뷰

- 내비게이션 스택을 이용해 콘텐츠 뷰들을 관리하는 컨테이너 뷰

- 스타일에 따라 UINavigationController 또는 UISplitViewController의 역할 수행

- 내비게이션 뷰는 콘텐츠 뷰를 스택처럼 감싸 주기만 하면 된다.

   ```swift
   NavigationView {
   	Image("SwiftUI")
   }
   ```

#### 내비게이션 바 타이틀(NavigationBarTitle)

- 내비게이션 제목을 표현할 수 있는 수식어

- 내비게이션 뷰를 수식하는 것이 아닌 그 내부에서 사용해야 한다.

   ```swift
   // 잘못된 방법
   NavgationView { ... }.navigationBarTitle("내비게이션 바 타이틀")
   
   //옳은 방법
   NavgationView { 
   	...
   		.navigationBarTitle("내비게이션 바 타이틀")
   }
   ```

   <br />

#### 내비게이션 바 아이템(NavigationBarItems)

- UIBarButtonItem의 역할을 수행하는 것으로, 각 아이템을 버튼으로 정의하여 navigationBarItems 수식어에 전달

- leading이나 trailing 위치에 둘 이상의 아이템을 넣어야 한다면, HStack을 이용해서 버튼 정의

#### 내비게이션 링크(NavigationLink)

- 지정한 목적지로 이동할 수 있도록 만들어진 버튼

- 뷰를 눌렀을 때 또는 미리 지정된 특정 조건을 만족했을 때 화면 전환

- UINavigationController의 pushViewController 메서드 기능을 수행하는 것과 동일

#### Hidden 수식어

- 필요에 따라 내비게이션 바 또는 뒤로 가기 버튼을 숨길 수 있다.

<br />

| 구분 | 설명 |
 | --- | --- |
| DefaultNavigationViewStyle | 내비게이션 뷰 기본 스타일, 내비게이션 뷰가 사용된 환경에 따라 자동으로 스타일 결정, watchOS 제외 모든 플랫폼 사용 가능 |
| StackNavigationViewStyle | 내비게이션 계층 구조를 하나의 뷰만으로 탐색해 나가는 스타일, UINavigationController가 사용, iOS와 tvOS만 사용 가능 |
| DoubleColumnNavigationViewStyle | Master와 Detail로 구분되는 2개의 칼럼(뷰)를 이용해 콘텐츠를 표현하는 스타일, watchOS 제외 모든 플랫폼 사용 가능, 내부적으로 SplitViewController 사용, 이 스타일을 사용할 수 없는 기기는 StackNavigationViewStyle로 전환 |
|     |     |

<br />

### 리스트(List)

- 하나의 열에 여러 개의 행으로 표현되는 UI를 구성해 다중 데이터를 쉽게 나열할 수 있도록 구성된 뷰

- 정적 콘텐츠 : 리스트의 생성자에 원하는 뷰를 전달하면 하나씩 각 로우에 담아 표현

- 동적 콘텐츠

   - Range<Int> : 범위만큼 로우 생성

   - RandomAccessCollection : RandomAccesCollection 프로토콜을 준수하는 데이터 제공

      - 데이터의 각 요소들을 구분하고 식별할 수 있도록 반드시 2가지 방법 중 하나를 택해 id 값을 제공

         - id 식별자 지정 : id로 사용할 값을 직접 인수로 제공, Hashable 프로토콜을 준수하는 프로퍼티 지정 가능, 그 데이터 타입 자체가 Hashable을 준수한다면 간단히 self로 입력 가능

         - identifiable 프로토콜 채택: 매개 변수에 id를 전달하는 대신 데이터 타입 자체에 identifiable 프로토콜 채택, 타입 자체에 id 프로퍼티를 만들고 이것을 식별자로 삼는다.

         <br />

#### 섹션(Section)

- 리스트는 섹션을 이용해 데이터를 쉽게 그룹화하는 것도 가능

   | 구분 | 설명 |
    | --- | --- |
   | DefaultListStyle | 리스트 기본 스타일. 사용 환경에 따라 적절한 스타일 결정 |
   | PlainListStyle | 데이터 목록을 각 행마다 하나씩 나열하는 형태의 기본 스타일, 모든 플랫폼 사용 가능 |
   | GroupedListStyle | 각 섹션을 분리된 그룹으로 묶어 표현하는 스타일. 사용 환경에 따라 grouped 또는 insetGrouped 스타일 중 하나가 자동으로 선택. iOS와 tvOS에서만 사용 가능 |
   |     |     |

   <br />

### 지오메트리 리더(GeometryReader)

- 자식 뷰에 부모 뷰와 기기에 대한 크기 및 좌표계 정보를 전달하는 기능을 수행하는 컨테이너 뷰

- 지오메트리 리더에 자식 뷰가 하나만 있을 때는 중앙에 정렬되지만, 두 개 이상 사용되면 좌상단을 기준으로 배치

- 크기를 지정하지 않으면, 주어진 공간 내에서 최대 크기를 가진다.

#### 지오메트리 프록시(GeometryProxy)

- 지오메트리 리더의 레이아웃 정보를 자식 뷰에 제공

   | 구분 | 설명 |
    | --- | --- |
   | size | 지오메트리 리더의 크기를 반환 |
   | safeAreaInsets | 지오메트리 리더가 사용된 환경에서의 안전 영역에 대한 크기 반환 |
   | frame(in:) | 특정 좌표계를 중심으로 한 프레임 정보 제공 |
   | subscript(anchor:) | 자식 뷰에서 anchorPreference 수식어를 이용해 제공한 좌표나 프레임을 지오메트리 리더의 좌표계를 기준으로 다시 변환하여 사용하는 첨자 이때 Anchor의 제네릭 매개 변수는 CGRect 또는 CGPoint 타입 두 가지 사용 가능 |

- frame

   - 지오메트리 프록시는 프레임에 대한 정보도 제공

   - 단순 자신의 CGRect 값을 전달하는 것이 아닌 CoordinateSpace라는 열거형 타입이 가진 세 가지 값 중 하나를 지정하면 그 좌표 공간에 대한 정보 반환

      ```swift
      enum CoordinateSpace {
      	case global
      	case local
      	case named(AnyHashable)
      }
      ```

      | 구분 | 설명 |
       | --- | --- |
      | global | 화면 전체 영역(윈도우의 bounds)을 기준으로 한 좌표 정보 |
      | local | 지오메트리 리더의 bounds를 기준으로 한 좌표 정보 |
      | named | 명시적으로 이름을 할당한 공간을 기준으로 한 좌표 정보 |

      <br />

   #### 프레임 수식어

   - UIKit에서 뷰에 프레임을 설정했던 것과는 사뭇 다르다

   - SwiftUI에서의 프레임은 예전 방식과 같이 제약 조건을 설정하는 것이 아니라, 액자처럼 콘텐츠를 담고 있는 하나의 뷰라는 점을 인식해야 한다.

   - SwiftUI에서 프레임은 자식 뷰가 사용 가능한 크기를 제안하기 위해 사용

   - 동시에 뷰의 정렬 위치를 결정하는 역할도 함

   - 다만, 제안된 공간 내에서 실제로 자식 뷰가 어느 정도 크기를 가지고 어떻게 보일 지는, 그 뷰가 직접 결정

   #### 뷰 레이아웃 과정

   - 부모 뷰가 활용 가능한 크기를 자식 뷰에 제안

   - 자식 뷰는 그 자신의 크기를 결정

   - 부모 뷰는 자신의 좌표 공간에서 자식 뷰를 적절히 배치

   #### 고정 크기 vs 크기 제약 조건

   - 고정 크기 : width, height 중 하나 또는 둘 다 값을 입력해 항상 고정된 크기를 가지게 할 때 사용

   - 크기 제약 조건 : 고정된 값을 입력하는 대신 최소나 최대 또는 이상적인 값에 대한 제약 조건을 입력하는 방법

   #### Layout Priority

   - 레이아웃의 우선순위가 높을 경우 부모 레이아웃이 자식에 공간을 할당함에 있어 형제 뷰 그룹 내에서 우선권을 가진다. 

   - 이 경우 부모 뷰의 공간이 늘어날 때 다른 형제 뷰보다 더 빨리 늘어나고, 줄어들 때는 더 늦게 줄어든다.

