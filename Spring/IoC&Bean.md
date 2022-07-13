# Spring IoC/DI 와 Bean 


## 1. IoC / DI 란?

- IoC란 Inversion of Control의 줄임말이며, 제어의 역전이라고 한다.

     (이를 스프링 컨테이너가 코드 대신 오브젝트에 대한 제어권을 갖고 있다고 해서 IoC라고 부른다.)

- Spring에서 사용되는 IoC란 객체가 내부적으로 조작할 객체를 직접 생성하지 않고 외부로부터 주입받는 기법을 의미한다. 

- 이때 객체를 외부로부터 주입해주는 작업을 `DI(의존성 주입)`이라고 부른다.

![img](https://user-images.githubusercontent.com/91296293/178726972-1f34d885-6e65-41d4-8029-b30e0cfc2789.jpg)


## 2. IoC Container란? 

 - IoC Container는 오브젝트의 생성과 관계설정, 사용, 제거 등의 작업을 대신 해준다하여 붙여진 이름이다. </br>
 
   (이때, IoC Container에 의해 관리되는 오브젝트들은 Bean 이라고 부른다.) 
   
 - IoC Container는 Bean을 저장한다고 하여, BeanFactory 라고도 불린다. BeanFactory는 하나의 인터페이스이며, Application Context는 BeanFactory의 구현체를 상속받고 있는
  인터페이스이다. 실제로 스프링에서 IoC Container 라고 불리는 것은 Application Context의 구현체이다.

<img width="276" alt="images_lsj16632_post_25c1130a-5d49-4dd6-8857-56dbbcd54fbe_스크린샷 2021-12-20 오후 2 45 05" src="https://user-images.githubusercontent.com/91296293/178727836-ff33724f-c7a7-4223-a463-be7f5b02e67f.png">


## 3. Spring DI/IoC 는 어떻게 동작하나?

- IoC(제어의 역전)은 프로그램의 제어 흐름을 직접 제어하는 것이 아니라 외부에서 관리하는 것으로 코드의 최종호출은 개발자가 제어하는 것이 아닌 *프레임워크의 내부에서 결정된 대로* 이루어진다. 

- DI(의존관계 주입)은 Spring 프레임워크에서 지원하는 IoC의 형태로 클래스 사이의 의존관계를 빈 설정 정보를 바탕으로 컨테이너가 자동으로 연결해준다.

- 스프링에서는 스프링 컨테이너 `ApplicationContext`를 이용하여 설정 정보를 생성, 등록하고 필요한 객체를 생성자 혹은 setter를 통해 주입한다. 




## 4.  IoC 컨테이너의 역할

- 객체의 생성을 책임지고, 의존성을 관리해준다. 그래서 개발자들은 비즈니스 로직에 집중할 수 있다. 





## 5. Spring Bean이란



- IoC 컨테이너에 의해 관리되는 오브젝트들은 Bean 이라고 부른다. 
- IoC 컨테이너 안에 들어있는 객체로 필요할 때 IoC컨테이너에서 가져와서 사용하며 @Bean 을 사용하거나 xml설정을 통해 일반 객체를 Bean으로 등록할 수 있다.





## 6. Spring Bean 의 생성과정 

- 객체 생성 → 의존 설정 → 초기화 → 사용 → 소멸 과정의 생명주기를 가지고 있다.

- 스프링 컨테이너가 초기화 될 때 먼저 빈 객체를 설정 정보에 맞추어 생성하고, 의존 관계를 설정한 뒤에 해당 프로세스가 완료되면 빈 객체가 지정한 메소드를 호출해서 초기화한다.객체를 사용한 뒤 컨테이너가 종료 될 때 빈이 지정한 메소드를 호출해 소멸 과정을 진행한다.



 ### 1. 빈 초기화, 소멸 (Initialize & Destory)



  - 빈 초기화방법은 @PostConstruct 를 빈 소멸에서는 @PreDestroy 를 사용한다.





`@PostConstruct`

- 초기화하고 싶은 메서드에 @PostConstruct 애노테이션을 붙여주면 Spring이 해당 메서드를 초기화시에 호출하게 된다.


```java
@Slf4j
@Component
public class SimpleBean {

    @PostConstruct
    public void postConstruct() {
        log.info("postConstruct");
    }
}
```

`@PreDestroy`

-컨테이너가 종료될 때 실행하고 싶은 메서드에 애노테이션을 붙여주면 Spring이 컨테이너 종료 시 해당 메서드를 호출한다.


```java
@Slf4j
@Component
public class SimpleBean {

    @PreDestroy
    public void preDestroy() {
        log.info("preDestroy");
    }
}
```

### 2. 빈 등록



- 생성한 스프링 빈을 등록할 때는 ComponentScan을 이용하거나 @Configuration 의 @Bean 을 사용하여 빈 설정파일에 직접 빈을 등록할 수 있다.



- 컴포넌트 스캔의 원리는 기본적으로 @Component 어노테이션이 있으면 자동으로 스프링 빈으로 등록된다. 참고로, @Component 어노테이션은  @Controller , @Service, @Repository를 포함한다.


```java
@Controller 
public class MemberController {

    private final MemberService memberService;
    @Autowired
    //멤버 컨트롤러가 생성이 될떄 스프링빈에 등록되어있는 멤버서비스를 주입
    public MemberController(MemberService memberService) {
        this.memberService = memberService;
    }
}
```

- @Configuration 어노테이션을 추가하고, 스프링 빈으로 등록하고자 하는 Service와 Repository에 @Bean 어노테이션을 추가하면, 스프링 빈으로 등록된다.


```java
@Configuration
public class SpringConfig {

    @Bean
    public MemberService memberService() {
        return new MemberService(memberRepository());
    }

    @Bean
    public MemberRepository memberRepository(){
        return new MemoryMemberRepository();
    }
}
```


## 7. Spring Bean의 Scope 이란



- 빈 스코프는 빈이 존재할 수 있는 범위를 뜻이다.

- [종류]: 싱글톤, 프로토타입, request, session, application 등



`싱글톤` : 기본 스코프로 스프링 컨테이너의 시작과 종료까지 유지되는 가장 넓은 범위의 스코프

`프로토타입` :빈의 생성과 의존관계 주입까지만 관여하고 더는 관리하지 않는 매우 짧은 범위의 스코프</br>
`request` : 웹 요청이 들어오고 나갈때까지 유지하는 스코프</br>
`session` : 웹 세션이 생성, 종료할때까지 유지하는 스코프</br>
`application` : 웹 서블릿 컨텍스트와 같은 범위로 유지하는 스코프

-------------------------------------







출처:

https://1-7171771.tistory.com/105

https://github.com/ksundong/backend-interview-question

https://ooeunz.tistory.com/107

