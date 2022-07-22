# Java Basic

### JVM(Java Virtual Machine) 동작 방식

![image](https://user-images.githubusercontent.com/55472510/180148232-8853d53b-cf9d-4dbe-ba74-1bf3f3f28b88.png)

`(1) Class Loader`
JVM내로 클래스 파일을 로드하고, 링크를 통해 배치하는 작업 수행

`(2) Execution Engine`
class loader를 통해 JVM 내의 Runtime Data Area에 배치된 바이트 코드드을 명령어 단위로 읽어서 실행함

`(3) Garbage Collector`
heap 메모리 영역에 생성된 객체들 중 참조되지 않은 객체들을 탐색 후 제거하는 역할

`(4) Runtime Data Area`
JVM의 메모리 영역으로 자바 애플리케이션을 실행할 때 사용되는 데이터들을 적자하는 영역

    - Method Area: 모든 스레드가 공유하는 메모리 영역으로 class, interface, method, field, static변수 등의 바이트 코드 보관
    - Heap Area: 모든 스레드가 공유하며, new 키워드로 생성된 객체와 배열이 생성되는 영역
    - Stack Area: 메서드 호출시 각각 스택 프레임이 생성됨-> 메서드 안에서 사용되는 값들을 저장하고, 매개변수, 지역변수, 리턴값 및 연산시 일어나는 값들을 임시로 저장 -> 메서드 수행 종료 후 프레임 별로 삭제
    - PC Register: 스레드 시작시 생성되며, 생성되는 공간으로 스레드 마다 하나씩 존재함/ 어떤 부분을 무슨 명령으로 실행해야할 지에 대한 기록을 하는 부분으로 현재 수행중인 JVM명령의 주소를 가짐
    - Native Method Stack: 자바외 언어로 작성된 네이티브 코드를 위한 메모리 영역

<br/>

### Garbage Collector(GC)

`자바의 메모리 관리 방법 중 하나로, JVM의 Heap 영역에서 동적으로 할당했던 메모리 영역 중 필요 없게 된 메모리 영역을 주기적으로 삭제하는 프로세스`

- Stop-The-World: GC가 일어나면 GC를 담당하는 스레드를 제외한 모든 스레드들은 작동이 일시적으로 정지되게 됨 -> 더 이상 작업이 실행되지 않고, 성능이 저하됨

- Major GC & Minor GC
  GC가 일어나는 시점에 따라 분류

        Minor GC: JVM의 Young영역에서 발생 /상대적으로 시간이 짧아서 stop-the-world가 이루어지지 않는 다고 간주(stop-the-world가 발생하긴 하지만 아주 짧은 시간만 발생하여 없다고 간주하는 것)
        Major GC: Old 영역에서 발생하고, 상당히 긴 시간동안 stop-the-world가 발생하고, 프로그램에 영향을 준다

  <br/>

### Collection

![image](https://user-images.githubusercontent.com/55472510/180153264-ff729007-fb4d-4f1d-a280-9f26692bd511.png)

<br/>
### Generic

`클래스 내부에서 지정하는 것이 아닌 외부에서 사용자에 의해 지정되는 것을 의미`

#### 장점

(1) 잘못된 타입이 들어올 수 있는 것을 컴파일 단계에서 방지할 수 있음
(2) 클래스 외부에서 타입을 지정해주기 때문에 따로 체크하고 변환해줄 필요가 없다-> 관리가 편하다
(3) 비슷한 기능을 지원하는 경우 코드의 재사용성이 높아짐

| 타입 | 설명    |
| ---- | ------- |
| <T>  | Type    |
| <E>  | Element |
| <K>  | Key     |
| <V>  | Value   |
| <N>  | Number  |

```Java
public class Name <T,k>{...}//type &key
public Interface name <T>{...}//type

public class Main{
    public static void main(String []args){
        Name <String ,Integer> a = new Name<String, Integer>();
    }
}
```

<br/>

### Interface 와 abstract class의 차이

1. 추상클래스란?
   추상 메서드를 선언하여 `상속을 통해서 자손 클래스에서 완성하도록 유도`하는 클래스
   따라서 상속을 위한 클래스이기 때문에 따로 객체를 생성할 수 없다

```Java
abstract class name{
    public abstract void a();
}
```

2. 인터페이스란?
   기본설계도라고 할 수 있으며 다른 클래스를 작성하는데 도움을 주는 목적으로 작성하고 클래스와 다르게 다중상속(구현)이 가능

```Java
interface names{
    public static final a = 6;
    public abstract void b();
}
```

3.공통점과 차이점 - 공통점: method의 선언만 있고, 구현내용이 없음 - 차이점: 추상 클래스는 extends 키워드를 사용하여 상속하고, `다중상속하는 것이 불가능`함/ 반면에 인터페이스의 경우 implements 키워드를 사용하여 상속하고, `다중상속이 가능`함

<br/>

### 동등성과 동일성

- 동등성(equality): 동등하다는 뜻으로 두 개의 객체가 같은 정보를 갖고 있는 경우-> equals()를 사용할 수 있음
- 동일성(identity): 동일하다는 뜻으로 두 개의 객체가 완전히 같은 경우-> 주소 값 이 같기 때문에 두 변수가 같은 객체를 가리키게됨 -> ==연산자로 비교

### 출처

JVM: https://steady-coding.tistory.com/305
GC: https://tecoble.techcourse.co.kr/post/2021-08-30-jvm-gc/
Collection: https://gangnam-americano.tistory.com/41
Generic: https://st-lab.tistory.com/153
추상클래스: https://myjamong.tistory.com/150
https://wildeveloperetrain.tistory.com/112
동등성과 동일성: https://steady-coding.tistory.com/534
