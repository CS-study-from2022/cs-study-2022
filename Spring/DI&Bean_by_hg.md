# Spring DI & Bean

> Question List

1. DI 종류는 어떤 것이 있고, 이들의 차이는?

2. Autowiring 의 과정에 대해 설명해 보자

3. Bean/Component 어노테이션에 대해서 설명하고, 차이점에 대해 설명해보자

4. 의존성과 설정값을 생성자 인자로 주입해야하는 이유는?

<hr/>

## IoC(Inversion of Control: 제어의 역전)

일반적으로 코드를 짤 때 개발자가 직접 의존성을 주입한다

```Java
public class IndexController{
    private ARepository  A= new ARepository();
}
```

위의 예시와 같이 직접 new 를 해서 의존성을 주입했다

하지만 _제어의역전(IoC)의 경우 이와는 다르다_

외부에서 의존성을 주입한다는 뜻이다

즉, *DI(Dependency Injection)이 IoC의 일종*이다

_의존성을 역전시켜 객체간의 결합도를 줄이고 유연한 코드를 작성할 수 있게 만들어 코드의 중복을 줄이고 유지보수에 편리하다_

스프링이 모든 의존성 객체를 실행될 때 만들어주고 필요한 곳에 주입시켜 **Bean은 싱글턴 패턴의 특징을 가지며**, 개발자가 아닌 스프링에게 맡기게 되는 것이다

<hr/>

## DI(Dependency Injection) in Spring

- 강한 결합 : 객체 내부에서 다른 객체를 생성하는 것 -> A에서 B를 직접 생성하고 있다면, B를 바꾸고 싶은 경우에 A도 수정해야하는 방식

- 느슨한 결합 : 외부에서 생성된 객체를 Interface를 통해서 넘겨 받는 것 -> 결합도를 줄일 수 있고, 유지보수성이 증가함

- 의존성 주입을 사용하는 이유
  1. 재사용성 증가
  2. 테스트에 용이
  3. 코드의 단순화 -> 가독성 증가
  4. 종속성의 감소로 변경시 민감하지 않음
  5. 유연성과 확장성 향상

<hr/>

### 의존성 주입(Dependency Injection) 방법 3가지

1. Field Injection (필드 주입)

변수 선언부에 `@Autowired` Annotation을 붙인다

```Java
@Component
public class indexContoller
{
    @Autowired
    private indexService indexService;
}
```

- 사용하면 안되는 이유

  1. 의존성을 주입하기가 쉽다
  2. Constructor의 parameter가 많아짐과 동시에 하나의 class가 많은 책임을 떠안는다
  3. 순환의존성을 발생시킬 수 있다

2. Setter Injection(수정자 주입)

선택적인 의존성을 사용할 때 유용하다

```Java
@Component
public class indexContoller
{
    @Autowired
    public void setIndexService(indexService indexService)
    {
        this.indexService= indexService;
    }
}
```

의존 관계 주입은 런타임시 할 수 있도록 낮은 결합도를 갖게된다

하지만 Controller객체는 여전히 생성 가능하기 때문에 NPE가 발생할 수 있다

3. Constructor Injection (생성자 주입)

```Java
@Component
public class indexService
{
    private indexDAO indexDAO;

    @Autowired
    public indexService(indexDAO indexDAO){
        this.indexDAO = indexDAO;
    }

}

@Component
public class indexController{
    private final indexService indexService = new indexService(new indexDAO());
}
```

가장 권장되는 방식으로 필수적으로 사용해야하는 레퍼런스 없이는 인스턴스를 만들지 못하도록 강제하기 때문이다

## Autowiring 과정

`BeanPostProcessor`라는 라이프 사이클 interface의 구현체인 `AutowiredAnnotationBeanPostProcessor`에 의해 의존성 주입이 이루어진다

`BeanPostProcessor`는 초기화 라이프 사이클 이전, 이후에 필요한 부가 작업을 할 수 있는 라이프 사이클 콜백이다

따라서 `AutowiredAnnotationBeanPostProcessor`가 Bean의 초기화 라이프 사이클 이전, 빈의 생성 이전에 어노테이션을 보고 해당하는 빈을 찾아 주입해주는 것이다

<hr/>

## Bean/Component Annotation에 대해 설명하고, 차이점에 대해서 정리해보자

우선 두 annotation 모두 Spring(IOC) Container에 Bean을 등록하도록 하는 메타데이터를 기입하는 어노테이션이다

### 차이점

- @Bean: method레벨에서 선언하며, 반환되는 객체를 개발자가 수동으로 bean으로 등록하는 어노테이션이다

  +) 개발자가 컨트롤이 불가능한 외부 라이브러리들을 bean으로 등록하고 싶은 경우에 사용

- @Component: class 레벨에서 선언함으로써 스프링이 런타임시 component-scan을 통해 자동으로 bean을 찾고 등록하는 어노테이션이다

  +) 개발자가 직접 컨트롤이 가능한 class들의 경우엔 @component를 사용

<hr/>

## 의존성과 설정값을 생성자 인자로 주입해야하는 이유는?

1. `NullPointException을 방지`할 수 있다
2. 주입받을 field를 `final로 선언 가능`하다 -> 객체 생성 시점에 초기화가 이루어져서 쉽게 필수 의존관계를 파악할 수 있다(Immutable)
3. Spring에서는 `순환참조를 방지`할 수 있다

   +) 순환참조: A가 B에 의존하고 B가 A에 의존하는 경우

4. 테스트 코드를 작성하기 좋다

5. `단일책임원칙(SRP)`: field injection은 의존성 주입이 쉬우므로, 무분별한 DI가 가능하다. 이렇게 되면 하나의 클래스에서 지나치게 많은 기능을 하게 될 수 있기때문에, 단일책임원칙이 깨지기 쉽다

6. `DI Container와의 낮은 결합도` : Constructor Injection은 생성자로 의존성을 주입받기 때문에 DI Container에 의존하지 않고 사용할 수 있기 때문에 테스트에서 용이하다

요약: `불변성(Immutable)`과 누락방지를 보장해주기 때문

<hr/>

> 출처

<https://velog.io/@gillog/Spring-DIDependency-Injection-%EC%84%B8-%EA%B0%80%EC%A7%80-%EB%B0%A9%EB%B2%95>

<https://atoz-develop.tistory.com/entry/Spring-Autowired-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC-BeanPostProcessor>

<https://galid1.tistory.com/494>

<https://velog.io/@woply/spring-%EC%83%9D%EC%84%B1%EC%9E%90%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EC%9D%98%EC%A1%B4-%EA%B4%80%EA%B3%84-%EC%A3%BC%EC%9E%85%EC%9D%84-%EA%B6%8C%EC%9E%A5%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0>

<https://tecoble.techcourse.co.kr/post/2020-07-18-di-constuctor-injection/>
