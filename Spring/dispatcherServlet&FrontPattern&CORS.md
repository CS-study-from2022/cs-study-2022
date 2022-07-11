
## Spring Web MVC의 Dispatcher Servlet의 동작원리
* Dispacter Servlet이란
    * HTTP 프로토콜로 들어오는 모든 요청을 **가장 먼저 받아** 적합한 컨트롤러에 위임해주는 프론트 컨트롤러

<br>

* 장점
    1. 과거에는 모든 서블릿을 매핑하기 위해 web.xml에 등록해야 했지만 dispacter servlet이 모든 요청을 알아서 매핑해줌
    2. 요청을 먼저 받아 공통 작업을 처리할 수 있음

<br>

![image](https://user-images.githubusercontent.com/56907015/178278968-c2ac0326-8685-40fe-81c0-fc576fe1cc5e.png)  
* Dispatcher servlet: 클라이언트의 요청을 디스패처 서블릿이 받음
* Handler Mapping: 요청을 위임할 컨트롤러를 찾음 
* Dispatcher servlet => Handler Adapter: 요청을 컨트롤러로 위임할 어댑터를 찾아 전달
* Handler Adapter => RestController: 컨트롤러로 위임
* RestController: 비지니스 로직 처리 
* RestController => Handler Adapter : 반환값 전달
* Handler Adapter: 반환값 처리
* Hander Adapter => Dispacter Servlet: 반환값 전달
* Dispacter Servlet: 서버의 응답을 클라이언트로 반환

<br>

## 프론트 컨트롤러 패턴
* 각 요청을 프론트 컨트롤러가 먼저 받아 요청에 맞는 컨트롤러를 찾아 호출시키는 패턴
* Spring의 Dispacter servlet이 이에 해당

<br>

* 장점
    * 공통 로직을 먼저 처리할 수 있음
    * 컨트롤러를 구현할 떄 직접 서블릿을 다루지 않아도 됨

<br> 

## CORS 에러 해결
* 교차 출처 리소스 공유(Cross-Origin Resource Sharing, CORS)    
    * 다른 출처의 자원을 공유할 수 있도록 설정하는 권한 체제

<br>

* CORS 에러 해결 방법
    1. Configuration: WebConfig 클래스를 생성하여 CorsRegistry의 addMapping을 통해 URL 패턴 정의 가능
    2. Annotation: @CrossOrigin(origin= " " , allowedHeader=" ")를 통해 추가 



<br>
<br>

* 출처
   * dispatcher servlet: https://mangkyu.tistory.com/18
   * 프론트 컨트롤러 패턴: https://velog.io/@suhongkim98/Front-Controller-%ED%8C%A8%ED%84%B4%EA%B3%BC-spring-MVC
   * CORS: https://wonit.tistory.com/572
