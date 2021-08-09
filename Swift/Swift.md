# Swift

### 스위프트 언어의 특징

- 빠름(Fast)

   - 복합정렬 벤치마크를 보면 파이썬보다 대략 3.9배 빠름, Objc보다 약 2.8배 빠름

   - LLVM 컴파일러에서 제공하는 코드 최적화기를 사용해 소스 컴파일과 최적화를 수행

- 설계에 의한 안정성(Safety by Design)

   - 변수나 상수는 반드시 선언한 후에 사용하도록 강제

   - 타입 추론 기능에 의해 변수의 초기값을 기준으로 타입 정의

   - 배열과 정수는 오버플로우에 대비하여 확인

   - 개발자가 정의하지 않은 배열 값에 승인하지 않은 값들이 주입될 수 없도록 Array bounds check

   - 포인터에 직접 접근하는 시도 차단, 클래스를 통해 간접적으로만 레퍼런스 참조하도록 제한

   - ARC를 이용해 자동으로 메모리 관리

- 현대적(Modern)

   - 파이썬 언어에 기반을 둔 읽고 쓰기 쉬운 문법

   - 헤더 파일 사용 대신 메인 파일에 통합하여 코드 작성

- 상호반응(Interactive)

- 완전한 플랫폼(Complete Platform)

   - Objc 코드에 의존하지 않고도 프로그램 작성 가능

- 통합(Unified)

<br />

### 스위프트의 기초 문법 특징

- 헤더 파일을 작성할 필요가 없다.

   - 기존의 Objc는 헤더 파일과 메인 파일로 분리되어 있었지만, 스위프트는 헤더와 소스 파일이 통합된 하나의 *.swift 파일에 필요한 내용을 자유롭게 정의하고 사용

- 대소문자 구분

- 구문 끝의 세미콜론은 생략 가능

   - 한 줄에 두 개 이상의 구문을 작성할 때는 세미콜론을 붙여야 함

- 엔트리 포인트(시작점)으로 사용되는 main() 함수가 없음

   - 다만, @UIApplication 어노테이션을 사용해 앱을 시작하는 객체 지정

- String 뿐만 아니라 Character도 큰 따옴표 사용

- import 키워드를 사용하지만, 라이브러리와 프레임워크의 참조 용도

- C나 자바처럼 한 줄 주석, 여러 줄 주석 처리 방식을 모두 지원

   - // : 한 줄 주석

   - /* ~ */ : 여러 줄 주석

- try ~ catch 방식의 오류 처리 지원

<br />

### 변수와 상수

- 저장한, 혹은 저장할 메모리 주소값을 이름으로 연결해 놓은 것

- 둘 다 값을 저장할 수 있지만 상수는 한 번 저장된 값을 다른 값으로 변경할 수 없음

- 변수의 값을 변경할 수 있다고 하더라도 처음 저장했던 값과 일치하는 타입으로만 변경 가능

- 스위프트는 '타입 추론기'라는 기능 모듈을 컴파일러에 별도로 내장하여, 항상 최적의 타입을 결정

- 변수명, 상수명 정의

   - 알파벳과 한글 자음 및 모음, 아라비아 숫자, 특수 기호, 한자, 이미지용 바이너리 코드 모두 사용 가능 → 사용할 수 있다의 정도지 영어, 숫자, 밑줄 이외의 다른 문자나 기호 절대 쓰지 말것

   - 연산자와 혼동할 수 있는 +, -, *, / 및 공백은 사용할 수 없음(언더바는 가능)

   - 예약어나 키워드로 등록되어 있는 단어 사용 불가능. 단, 대소문자 변경 시 사용 가능

   - 첫 번째 자리에 숫자는 올 수 없음

### 기본 자료형(Data Types)

- Int

   - Int8, Int16, Int32, Int64 등으로 이어지는 int 계열 서브 자료형의 대표 자료형

   - 부호 있느 정수 자료형

   - 해당 컴퓨터의 CPU 비트 크기에 맞춰 자동으로 그 크기 변화

- UInt

   - 부호 없는 정수, 양수만 저장 가능

- Double & Float

   - 실수 값을 저장할 수 있는 자료형

   - Double : 64비트 부동 소수점 자료형 (소수점 아래 15~16자리)

   - Float : 32비트 부동 소수점 자료형 (소수점 아래 7~8자리)

- Bool

   - true / false 두 값만 가질 수 있는 논리값을 저장하는 자료형

- String

   - 문자열을 저장할 수 있는 집단 자료형

   - NSString과 String 사이의 타입 변환은 오류 발생 여지가 없는 완전 변환

- Character

   - 한 개의 문자를 저장할 수 있는 단일 자료형

   - Character 타입의 데이터 값을 표현할 때도 큰 따옴표 사용

   <br />

### 타입 어노테이션(Type Annotation)

- 변수나 상수를 선언할 때 타입을 명시적으로 선언해주는 것

- 변수나 상수명 뒤에 콜론(:)을 붙여서 타입 지정

- ex) var year: Int?

### 타입 추론(Type inference)

- 변수나 상수를 초기화할 때 입력된 값을 분석하여 변수에 적절한 타입을 컴파일러가 스스로 추론하는 기능

- 주어진 값이 타입 A와 타입 B에 동시에 속하는 경우, 더 넓은 범위의 타입으로 결정

- 더 작은 범위의 타입으로 정의하려면 반드시 타입 어노테이션을 통해 명시적으로 선언해야 함

### 문자열 템플릿

- 문자열에 변수를 포함시킬 때 좀 더 직관적이고편하게 사용하기 위한 기능

- "문자열 \(변수)"처럼 \() 안에 변수명을 넣어서 사용

### 쿼우팅(Quoting)

- 문자열을 따옴표로 묶어서 표시하는 방법

- 스위프트에서는 문자열, 문자 모두 "(큰따옴표)로 표시

- 멀티 라인 스트링

   - 스위프트 4.0부터 도입된 문법

   - 큰따옴표 세 개를 연속으로 붙여(""" ~ """) 그 내부에서 자유롭게 작성된 문자열을 실제 내용으로 처리하는 방식

   - 트리플 쿼우팅(Triple-Quoting)이라고 불리기도 함

   - 트리플 쿼우팅이 시작된 후에는 줄바꿈 후 입력을 시작해야 하고, 종료할 때에도 줄바꿈하여 쿼우팅을 닫아야 함

   <br />

### 연산자

<br />

| 구분 | 연산자 | 사용 예 | 의미 |
 | --- | --- | --- | --- |
| 단항 연산자 | - | -a | 값의 부호 변경 |
| 이항 연산자 | + | a + b | 두 개의 값을 더함 |
|     | - | a - b | 앞의 값에서 뒤의 값을 뺌 |
|     | * | a * b | 두 개의 값을 곱함 |
|     | / | a / b | 앞의 값을 뒤의 값으로 나눔 |
|     | % | a % b | 앞의 값을 뒤의 값으로 나눈 나머지 |

<br />

| 연산자 | 사용 예 | 의미 |
 | --- | --- | --- |
| < | a < b | a가 b보다 작으면 true |
| > | a > b | a가 b보다 크면 true |
| <= | a <= b | a가 b보다 작거나 같으면 true |
| >= | a >= b | a가 b보다 크거나 같으면 true |
| == | a == b | a가 b와 같으면 true |
| != | a != b | a와 b가 다르면 true |

<br />

| 연산자 | 사용 예 | 의미 |
 | --- | --- | --- |
| ! | !a | a가 true면 false 반환, false면 true 반환 |
| && | a && b | a와 b 모두 true면 true 반환 하나라도 false면 false 반환 |
| || | a || b | a와 b 둘 중 하나라도 true면 true 반환 둘 다 false면 false 반환 |
|     |     |     |

#### 범위 연산자

- 닫힌 범위 연산자(Closed range operator)

   - 주어진 피연산자 a, b를 포함하는 범위를 나타내는 연산자

   - ex) 1...5 : 1부터 5까지의 범위

- 반 닫힌 범위 연산자(Half-closed range operator)

   - 연산자 양쪽 경계 중 왼쪽 경계는 포함하되 오른쪽 경계는 포함하지 않는 연산자

   - ex) 1..<5 : 1부터 4까지의 범위

- 범위 연산자의 왼쪽에는 작은 숫자, 오른쪽에는 그보다 큰 숫자를 배치해야 한다 그렇지 않다면 런타임 오류가 뜨기 때문에 주의해야 함

<br />

| 연산자 | 사용 예 | 의미 |
 | --- | --- | --- |
| = | a = 1 | 변수 a에 1을 대입 |
| += | a += 1 | a = a + 1 |
| -=  | a -= 1 | a = a - 1 |
| *= | a *= 2 | a = a * 2 |
| /= | a /= 3 | a = a / 3 |
| %= | a %= 3 | a = a % 3 |
| <<= | a <<= 3 | a = a << 3 |
| >>= | a >>= 3 | a = a >> 3 |
| &= | a &= b | a = a & b |
| ^= | a ^= b | a = a ^ b |
| |= | a |= b | a = a  |

<br />

### 흐름 제어 구문

- 프로그램 실행 과정에서 실행 흐름을 능동적으로 제어하기 위한 목적으로 사용되는 구문

- 반복문 : 주어진 조건에 따라 특정 코드 블록을 반복적으로 실행

- 조건문 : 특정 조건이 성립할 경우 지정된 코드 블록이 실행되도록 제어

- 특정 지점의 코드로 실행 제어를 옮겨줌으로써 코드가 실행되는 순서를 제어

<br />

#### 반복문

- For 반복문

   - for <루프 상수> in <순회 대상> { <실행 구문> }

   - 순회 대상 데이터 타입

      - 배열

      - 딕셔너리

      - 집합

      - 범위 데이터

      - 문자열

   - 루프 상수 생략 가능 for _ in ~

- while 구문

   - while <조건식> { <실행 구문> }

   - 조건식을 만족하는 동안 계속 실행

- reepat ~ while 구문

   - repeat { 

         <실행 구문>

      }

      while <조건식>

   - 실행 구문의 수행을 최소 한 번 보장

   <br />

#### 조건문

- if 구문

   - if <조건식> { <실행 구문> }

   - 조건을 만족하면 코드 블록 실행

- guard 구문

   - guard <조건식 또는 표현식> else { <실행 구문> }

   - 결과가 false일 때 실행 구문 수행

   - 주로 후속 코드들이 실행되기 전 특정 조건을 만족하는지 확인하는 용도로 사용

   - 즉, 특정 조건을 만족하지 않은 채로 후속 코드를 실행하면 심각한 오류가 발생하는 경우, 전체 구문을 조기 종료하기 위한 목적으로 사용

- #available 구문

   - OS 버전과 기기를 체크하기 위한 구문

   - ex) if #available(iOS 9, OSX 10.10, watchOS 1, *) {}

- switch 구문

   - switch <비교 대상> {

         case <비교 패턴>:

         default:

      }

   - C나 자바와 문법이 유사하지만 C나 자바는 비교 패턴이 일치하는 경우 우선 실행 구문을 처리한 후 나머지 case에 대한 비교를 계속 진행하지만  스위프트는 일치하는 비교 패턴이 있을 경우 실행 코드 처리 후 전체 분기문 종료

   - 따라서 각 case 별로 break 구문 생략 가능

   - 암시적인 Fall Through 지원 X: 일치하는 case 블록을 실행하는 대신, 그 다음 case 블록으로 실행 흐름 전달

   - 대신 명시적으로 fallthrough 구문을 사용함으로써 Fall Through 지원

   - 스위프트에서는 case 키워드 다음에 하나 이상의 비교 패턴을 연이어 작성 가능

   - 튜플 내부의 아이템이 비교 대상과 부분적으로 일치하는 경우, 패턴 전체가 일치하는 것으로 간주

      ```swift
      var value = (2, 3)
      
      switch value {
      case let (x, 3):
      	print("튜플의 두 번째 값이 3일 때 첫 번째 값은 \(x)입니다")
      case let (3, y):
      	print("튜플의 첫 번째 값이 3일 때 두 번째 값은 \(y)입니다")
      case let (x, y):
      	print("튜플의 값은 각 \(x), \(y)입니다")
      }
      ```

   - 범위 연산자도 사용 가능

      ```swift
      var passtime = 1957
      
      switch passtime {
      case 0..<60:
      case 60..<3600:
      case 3600..<86400:
      default:
      }
      ```

   <br />

   #### 제어 전달문

   - break : switch 구문에서의 실행 흐름이나 반복 실행 중인 루프를 조건식의 결과와 상관 없이 즉각 종료

   - continue : 이 구문 아래에 있는 실행 구문들을 건너 뛰고 다음 반복을 시작

   <br />

   <br />

   ### 집단 자료형

   - 배열(Array) : 순서에 따라 데이터가 정렬된 목록 형태의 자료형

   - 집합(Set) : 중복되지 않은 유일 데이터들이 모인 집합 형태의 자료형

   - 튜플(Tuple) : 종류에 상관없이 데이터들을 모은 자료형, 수정 및 삭제 불가능

   - 딕셔너리(Dictionary) : 배열과 유사하나 인덱스 대신 키(Key)를 사용하여 Key-Value로 연관된 데이터들이 순서 없이 모인 자료형

   <br />

   #### 배열

   - 배열에 저장할 아이템의 타입에는 제약이 없지만, 하나의 배열에 저장하는 아이템의 타입은 모두 같아야 함

   - 선언 시 배열에 저장할 아이템 타입을 명확히 정의해야 함

   - 배열의 크기는 동적으로 확장할 수 있음

   #### 집합

   - 내부적으로 해시 연산의 결과값을 이용해 데이터를 저장하므로 데이터 타입은 해시 연산을 할 수 있는 타입이어야 함

   - 기본 타입이 아닌 임의로 만든 타입을 집합으로 사용하려면 Hashable 프로토콜을 구현해야 함

   - 기본 집합 연산

      - intersection(_:) : 양쪽 집합에서 공통되는 아이템을 선택해 새로운 집합을 만드는 메소드(교집합)

      - symmetricDifference(_:) : 양쪽 집합 중에서 한 쪽에만 있는 아이템을 선택하여 새로운 집합을 만드는 메소드, 양쪽 집합에 공통으로 있는 아이템은 제외

      - union(_:) : 양쪽 집합에 있는 모든 아이템을 선택하여 새로운 집합을 만드는 메소드(합집합)

      - subtract(_:) : 한쪽 집합에 있는 아이템에서 다른 쪽 집합에도 속하는 공통 아이템을 제외하고 새로운 집합을 만드는 메소드(차집합)

   - 부분집합과 포함관계 판단 연산

      - isSubset(of:) : 하나의 집합이 다른 집합의 부분집합인지 여부 판단

      - isSuperset(of:) : 하나의 집합이 다른 집합의 상위집합 역할을 하는지 판단

      - isDisjoint(with:) : 두 집합 사이의 공통 값이 없으면 true 하나라도 있으면 false

   #### 튜플

   - 여러 가지 타입의 아이템을 저장할 수 있지만, 선언되고 나면 상수적 성격을 띠므로 값을 추가하거나 삭제하는 등 변경 불가능

   - 하나의 아이템만 있는 튜플은 일반 자료형이 된다. ex) var tpl: (String) = ("tuple") == var tpl: String = "tuple"

   - 튜플의 아이템을 개별 변수나 상수로 각각 할당받는 바인딩 방식의 구문도 제공

   #### 딕셔너리

   - 고유 키(Key)와 그에 대응하는 값(Value)을 연결하여 데이터를 저장하는 자료형

   - 하나의 키는 하나의 데이터에만 연결

   - 키는 중복될 수 없음

   - 아이템에는 순서가 없지만 키에는 내부적으로 순서가 있으므로 for~in 구문으로 순회 탐색 가능

   - 키의 타입은 Hash 연산이 가능한 타입 즉, Hashable 프로토콜을 채택하고 구현한 타입

   <br />

   <br />

   <br />

### 옵셔널

- 값이 없음을 의미하는 특수한 값

- 언어 차원에서 프로그램의 안정성을 높이기 위해 사용

- Objc에서는 빈 메모리 주소를 가리키는 값이었지만 스위프트에서는 단순히 '값이 없음'을 의미

- 스위프트에서는 연산 과정에서 정상적으로 값을 처리하지 못하는 상황이 발생했을 때 오류 대신 nil을 반환

- 옵셔널 타입으로 선언된 자료형만 nil 값을 저장할 수 있음

- 옵셔널 타입 : 반환하고자 하는 값을 옵셔널 객체로 한번 더 감싼 형태 (옵셔널 래핑)

- 옵셔널 언래핑(Optional Unwrapping) : 옵셔널 타입을 해제하고 실제 값을 추출하는 것

<br />

#### 옵셔널 해제(Optional Unwrapping)

- 명시적 해제

   - 강제 해제

      - 옵셔널 타입의 값 뒤에 "!" 기호를 붙여주는 것, 강제 해제 연산자

      - 값이 nil인 경우 런타임 오류 발생

   - 비강제 해제

      - 옵셔널 바인딩 : if 구문 내에 조건식 대신 옵셔널 값을 일반 변수나 상수에 할당하는 구문을 사용하는 방식, guard 구문을 이용해도 옵셔널 바인딩 가능

         - if 구문을 사용한 옵셔널 바인딩 : if 구문의 코드 블럭 내에서만 해제된 값 사용 가능

         - guard 구문을 사용한 옵셔널 바인딩 : 실행 흐름 상 옵셔널 값이 해제되지 않으면 진행이 불가능할 정도로 큰일이 생길 때 사용하는 것이 좋음

- 묵시적 해제

   - 타입 어노테이션 뒤에 ? 대신 !를 붙여서 선언

   - 형식상 옵셔널로 정의해야 하지만, 실제로 사용할 때에는 절대 nil 값이 대입될 가능성이 없는 변수일 때 사용

<br />

<br />

## 함수

- 프로그램의 실행 과정 중에서 독립적으로 처리될 수 있는 부분을 분리하여 구조화한 객체

- 입력값을 받아 내부 처리 과정을 거친 후 그 결과값을 내어놓는 형태

- 일반 함수 : 프로그래밍 언어나 프레임워크 수준에서 제공하는 함수 (기본적으로 데이터의 처리나 연산 등을 수행하기 위한 목적)

- 사용자 정의 함수 : 우리가 원하는 기능을 실행해줄 함수를 직접 만들어 사용하는 함수
