## java의 장/단점
#### 장점
- 객체 지향 언어이다.
- 오픈 소스 라이브러리가 풍부하다.
- 특정 운영체제에 종속되지 않는다.
- JVM의 GC에 의한 자동 메모리 관리가 가능하다.
#### 단점
- 다른 기계어보다 상대적으로 속도가 느리다.
- 예외 처리를 개발자가 직접 해야 한다.

<br>

## OOP의 특징
- 추상화 : 객체의 공통 특징을 묶어서 필요한 부분만을 표현하기 위한 개념을 의미한다.
- 캡슐화 : 특정 목적을 위한 변수나 메소드를 하나로 묶는 것을 의미한다.
- 다형성 : 동일한 메소드에 다양한 객체를 대입해 다양한 결과를 얻어내는 성질을 의미한다.
- 상속 : 상위 클래스에 근거한 새로운 클래스 및 행위를 정의하는 개념을 의미한다.

<br>

## 접근제어자의 종류와 특징
- 변수 또는 메소드의 접근 범위를 설정해주기 위해 사용하는 Java 의 예약어를 의미한다.
> 1. public : 모든 접근 허용
> 2. protected : 동일 패키지 및 상속 관계의 하위 클래스에 대한 접근 허용
> 3. package : 패키지 내부 클래스에 대한 접근 허용
> 4. private : 클래스 내부 객체의 접근만 허용

<br>

## DTO와 VO의 차이
- DTO : 계층 간 데이터 전달을 위한 객체이다.
> * 필드 값이 같아도 같은 객체로 취급하지 않는다.
> * getter/setter 외의 로직이 필요없다.
- VO : 값 그 자체를 나타내는 객체이다.
> * 필드 값이 같으면 같은 객체로 간주한다.
> * getter/setter 외의 로직이 있어도 무방하다.

<br>

## 오버로딩과 오버라이딩의 차이
- 오버로딩 : 같은 이름의 메소드에서 인자의 수나 자료형이 다른 경우를 의미한다.
- 오버라이딩 : 상위 클래스의 메소드를 하위 클래스에 재정의하는 것을 의미한다.

<br>

## List, Set, Map의 차이
- List : 순서가 있는 Collection으로, 데이터 중복이 가능하다.
- Set : 순서가 없는 Collection으로, 데이터 중복이 불가능하다.
- Map : Key와 Value가 한 쌍으로 이루어져 있는 Collection이다.

## `==`와 `equals()`의 차이
- `==` : 대상의 주소값을 비교한다.
- `equals()` : 대상의 값 자체를 비교한다.

<br>

## Primitive Type(기본형)과 Wrapper Class(참조형)의 차이
- Primitive Type : 변수에 값을 그대로 저장한다.
> * 값을 `==`로 바로 비교할 수 있다.
> * int, float, double, boolean 등이 있다.
- Wrapper Class : 변수에 값을 객체 형태로 저장한다.
> * 값에 null을 허용할 수 있다.
> * Integer, Float, Double, Boolean 등이 있다.

<br>

- 출처
  - https://gmlwjd9405.github.io/2017/10/01/basic-concepts-of-development-java.html
  - https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Java
