## AOP란?
* AOP(Aspect Oriented Programming) 는 관점 지향 프로그래밍을 의미한다.
* 한 시스템에서 관점이 비슷한(=중복되는) 메서드들을 Aspect를 활용하여 모듈화하는 방식이다.
* 공통 로직을 핵심 비즈니스 로직과 분리하여 효과적으로 재사용하고자 하는 게 AOP의 목적이다.

> #### Aspect란?
> * 부가 기능을 추상화시켜 모아놓은 단위
> #### Spring AOP의 특징
> * 런타임 시점에 생성된 Proxy Bean이 Aspect 코드를 추가하도록 만들어진 프록시 패턴 기반의 AOP 구현체
> #### AOP의 정의 방식
> * Advice : 실질적인 로직을 의미
> * Pointcut : AOP의 적용 범위를 의미
> * Join point : AOP의 적용 시점을 의미

<br>

## Filter와 Interceptor의 개념 및 차이
* Filter, Interceptor, AOP 모두 프로그램의 실행 전후에 추가적인 행동을 할 때 사용되는 기능들이다.

![image](https://blog.kakaocdn.net/dn/1bEhb/btqH8cRq0sY/dQVkF7pbrdOTVnILW7bmzK/img.png)
* 요청에 따른 실행 순서 : Filter → Interceptor → AOP → Interceptor → Filter
> 1. Filter : Dispatcher Servlet 이전, 스프링 컨텍스트 외부에서 적용
> 2. Interceptor : 스프링 컨텍스트 내부에서 Controller에 관한 요청과 응답을 처리
> 3. AOP : 비즈니스 메서드의 전후 처리를 세밀하게 하고자 할 때 사용

<br>

## Filter와 Interceptor로 예외를 어떻게 처리할까?
* Filter : 클라이언트로부터 발생한 요청과 오류 페이지를 출력하기 위한 요청을 구분하는 DispatcherType을 활용해 예외를 처리할 수 있다.
> 1. Config Class에 `FilterRegistrationBean` 등록
> 2. Filter 구현체에서 `request.getDispatcherType()` 메서드로 요청 유형(`REQUEST`, `ERROR`) 확인 후 예외 처리
* Interceptor : 특정 경로를 포함하거나 제외하면서 예외를 처리할 수 있다.
> 1. Config Class에서 `addPathPatterns()`, `excludePathPatterns()` 메서드를 활용하여 적용 경로 설정
> 2. `preHandle()`, `postHandle()`, `afterCompletion()` 실행 시 예외 처리

<br>

## Spring Framework에서의 POJO란?
* POJO(Plain Old Java Object) 는 특정 자바 모델이나 기능, 프레임워크를 따르지 않는 Java Object를 지칭한다.
  * Getter, Setter만 있는 VO가  POJO의 대표적인 경우에 해당한다.
* "객체지향" 이라는 본래의 Java 장점을 극대화시킬 수 있다.
* 스프링 프레임워크는 IoC(Inversion of Control, 제어의 역전) 컨테이너를 기반으로 POJO를 가장 잘 활용할 수 있는 프레임워크 중 하나이다.

<br>

* 출처
   * AOP : https://yadon079.github.io/2021/spring/spring-aop-core
   * Filter, Interceptor : https://goddaehee.tistory.com/154
   * Filter, Interceptor 예외 처리 : https://develop-writing.tistory.com/97
   * POJO : https://siyoon210.tistory.com/120
