# Spring 기본 개념 

* [Spring Framework란?](#Spring-Framework란?)
  * [IoC란?](#Spring-Framework는-IoC-기반이다.-IoC란?)
  * [IoC의 구성요소 DI와 DL](#IoC의-구성요소-DI와-DL)
    * [Spring Framework의 특징 POJO](#Spring-Framework의-특징-POJO)
    * [Spring Framework의 특징 AOP](#Spring-Framework의-특징-AOP)
    * [Spring Framework의 특징 MVC](#Spring-Framework의-특징-MVC(Model-2))
    

## Spring framework란?

자바 플랫폼을 위한 오픈소스 애플리케이션 프레임워크로서 엔터프라즈급 애플리케이션을 개발하기 위한 모든 기능을 종합적으로 제공하는 경량화된 솔루션이다.
엔터프라이즈급 애플리케이션이란 기업을 대상으로 하는 개발이라는 말이다. 즉, 대규모 데이터 처리와 트랜잭션이 동시에 여러 사용자로부터 행해지는 매우 큰 규모의 환경을 엔터프라이즈 환경이라 한다.
**Spring Framework는 경량 컨테이너로 자바 객체를 담고 직접 관리**한다. 객체의 생성 및 소멸 그리고 라이프 사이클을 관리하며 언제든 Spring 컨테이너로부터 필요한 객체를 가져와 사용할 수 있다. 이는 Spring이 IoC 기반의 Framework라는 것을 의미한다.

### Spring Framework는 IoC 기반이다. IoC란?

IoC는 Inversion of Contorol의 약자로 말그대로 **제어의 역전**이다. <br/>

제어의 역전이란?

일반적으로 지금까지 프로그램은 "객체 결정 및 생성 -> 의존성 객체 생성 -> 객체 내의 메소드 호출"하는 작업을 반복했다.
이는 각 객체들이 프로그램의 흐름을 결정하고 각 객체를 구성하는 작업에 직접적으로 참여한 것이다.
**즉, 모든 작업을 사용자가 제어하는 구조**이다.

하지만, IoC에서는 이 흐름의 구조를 바꾼다. IoC에서의 객체는 자기가 사용할 객체를 선택하거나 생성하지 않는다. 또한 자신이 어디서 만들어지고 어떻게 사용되는지 또한 모른다.
자신의 **모든 권한을 다른 대상에 위임**함으로써 제어 권한을 위임받은 특별한 객체에 의해 결정되고 만들어진다.
**즉, 제어의 흐름을 사용자가 컨트롤하지 않고 위임한 특별한 객체에 모든 것을 맡긴다.**

**IoC란 기존 사용자가 모든 작업을 제어하던 것을 특별한 객체에 모든 것을 위임하여 객체의 생성부터 생명주기 등 모든 객체에 대한 제어권이 넘어간 것을 IoC, 제어의 역전**이라고 한다.

### IoC의 구성요소 DI와 DL 

**IoC란 DI와 DL에 의해 구현된다.

- DL(Dependency Lookup) - 의존성 검색
모든 IoC 컨테이너는 각 컨테이너에서 관리해야 하는 객체들을 관리하기 위한 별도의 저장소를 가진다. **Bean에 접근하기 위해 컨테이너에서 제공하는 API를 이용하여 사용하고자 하는 Bean을 Lookup하는 것**으로 컨테이너 API와 의존관계를 만이 가지면 가질수록 어플리케이션에 종속되는 단점이 있다.

- DI(Dependecy Injection) - 의존성 주입
DI는 Spring에서 새롭게 지원하는 IoC의 한 형태로써 각 계층 사이, 각 Class 사이에 필요로 하는 의존관계가 있다면, 이를 컨테이너가 자동적으로 연결시켜 준다. 각 Class 사이의 의존관계를 Bean 설정 정보를 바탕으로 컨테이너가 자동적으로 연결한다.

 ```
  - Setter Injection: Class 사이의 의존관계를 연결시키기 위해 Setter 메소드를 이용하는 방법
  - Constructor Injection: Class 사이의 의존관계를 연결시키기 위해 생성자를 이용하는 방법
  - Method Injection: Method Injection은 Setter Injection과 Constructor Injection이 가지고 있는 한계점을 극복하기 위하여 
    지원하고 있는 DI의 한 종류다. Singleton 인스턴스와 Non Singletone 인스턴스의 의존관계를 연결할 필요가 있을 때 사용한다.
```
<p align="center">
  <img src="https://t1.daumcdn.net/cfile/tistory/252FCF3B5231689B17" height="300" width="400">
</p>

### Spring Framework의 특징 POJO

POJO(Plain Old Java Object)로 말 그대로 평범한 자바 오브젝트이다.
이전 EJB(Enterprise JavaBeans)는 확장과 재사용이 가능한 로직을 개발하기 위해 사용 되었는데, EJB는 한가지 기능을 위해 불필요한 로직이 과도하게 들어가는 단점이 있다.
그래서 다시 조명을 받은 게 **POJO**이다. POJO는 getter/setter를 가진 단순 자바 오브젝트로 정의 한다.
이런 단순 오브젝트는 **의존성이 없고 추후 테스트 및 유지보수가 편리한 유연성의 장점**을 가진다. 이러한 장점들로 인해 객체지향적인 다양한 설계와 구현이 가능해지고 POJO의 기반의 Framework가 조명을 받고 있다.
Spring Framework 에서는 이러한 POJO을 지원하고 Spirng 홈페이지에는 이러한 글도 있습니다.

*POJO를 사용함으로써, 당신의 코드는 더욱 심플해졌고, 그로인해 테스트하기 더 좋으며, 유연하다. 요구사항에 따라 기술적 선택을 바꿀 수 있도록 바뀌었다.*

### Spring Framework의 특징 AOP

뒤에도 설명하겠지만, AOP(Aspect Oriented Programming)이란 말 그대로 관점 지향 프로그래밍이다.
대부분 소프트웨어 개발 프로세스에서 사용하는 방법은 OOP(Object Oriented Programming)이다.
OOP는 객체지향 원칙에 따라 관심사가 같은 데이터를 한 곳에 모아 분리하고 낮은 결합도를 갖게 하여 독립적이고 유연한 모듈로 캡슐화하는 것을 일컫는다.
하지만, 이런 과정 중 중복된 코드들이 많아지고 가독성, 확장성, 유지보수성을 떨어 뜨린다.
이런 문제를 보완하기 위해 나온 것이 AOP이다.
AOP에서는 **핵심 기능과 공통기능을 분리시켜 핵심 로직에 영향을 끼치지 않게 공통기능을 끼워 넣는 개발 형태**이다. 
이렇게 개발함에 따라 **무분별하게 중복되는 코드를 한 곳에 모아 중복되는 코드를 제거하여 한 곳에 보관함으로써 한 번의 수정으로 모든 핵심기능들의 공통기능을 수정할 수 있어 효율적인 유지보수가 가능하며 재활용성이 극대화**된다.
Spring에서는 AOP를 편리하게 사용할 수 있도록 이를 지원하고 있다.

### Spring Framework의 특징 MVC(Model 2)

<p align="center">
  <img src="https://t1.daumcdn.net/cfile/tistory/9929B2345B9E4E002D" height="300" width="500">
</p>

MVC(Model View Controller)란?
사용자 인터페이스와 비지니스 로직을 분리하여 개발하는 것이다. MVC에서는 Model 1과 Model 2가 나누어져 있으며 일반적인 MVC는 Model 2를 지칭한다.

- Model
Model에서는 데이터 처리를 담당하는 부분이다. Model 부분은 *Service 영역과 DAO 영역*으로 나누어진다.
여기서 중요한 것은 Service 부분을 불필요하게 HTTP 통신을 하지 않아야 하고, request나 response와 같은 객체를 매개변수로 받아선 안 된다.
또한, Model 부분의 Service는 view에 종속적인 코드가 없어야 하고, View 부분이 변경되더라도 Service 부분은 그대로 재사용할 수 있어야 한다.
**Model에서는 View와 Controller에 대한 어떠한 정보도 가지고 있어서는 안 된다.**

- View
View는 사용자 Interface를 담당하며 사용자에게 보여지는 부분이다. View는 Controller를 통해 모델의 데이터에 대한 시각화를 담당하며 View는 자신이 요청을 보낼 Controller의 정보만 알고 있어야 한다. **Model이 가지고 있는 정보를 저장해서는 안 되며 Model, Controller의 구성 요소를 알아서는 안 된다.**

- Controller
Controller에서는 View에게 받은 요청을 가공하여 Model(Service 영역)에 이를 전달한다. 또한, Model로부터 받은 결과를 View로 넘겨주는 역할을 한다. Controller에서는 모든 요청 에러와 모델 에러를 처리하며 **View와 Controller에 대한 정보를 알고 있어야 한다.**

이렇게 Model, View, Controller를 나누는 이유는, 소스를 분리함으로써 각 소스의 목적이 명확해지고 유지보수하는 데 있어서 용이하기 때문이다.
Model의 Service 영역은 자신을 어떠한 Controller가 호출하든 상관없이 정해진 매개변수만 받는다면 자신의 비지니스 로직을 처리할 수 있어야 한다.
즉, **모듈화를 통해 어디서든 재사용이 가능하여야 한다**는 뜻이다.
이 말은 View의 정보가 달라지더라도 Controller에서 Serivce에 넘겨줄 매개변수 데이터 가공만 처리하면 되기 때문에 유지보수 비용을 절감할 수 있는 효과가 있다.
또한 Service영역의 재사용이 용이하기 때문에 확장성 부분에서도 큰 효과를 볼 수 있는 장점이 있다.




---

# Spring AOP

* [Spring AOP - 기본](#Spring-AOP-기본)
  * [AOP 적용 타입](#AOP-적용-타입)

## Spring AOP 기본

### AOP (Aspect Oriented Programming)

예를 들어, doSomething이라는 메소드가 있다. 이 doSomething이라는 메소드의 실행 시간을 찍기 위해 timeCheck라는 메소드를 만들 수 있다.
``` java
public void timeCheck() {
  Stopwatch stopwatch = Stopwatch.createStarted();
  doSomething();
  stopwatch.stop();
  log.info("time : " + stopwatch.elapsed(MILLISECONDS);
}

public void doSomething() {
  ...
}
```

timeCheck 메소드의 flowchart는 아래와 같다.

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZ1mvK%2FbtqE01yTQyo%2FajxKAJMMKmUZCa71mtfqxK%2Fimg.png" height="400" width="400">
</p>

실제 우리의 비지니스 로직은 doSomething 메소드 뿐이며, 나머지는 부가적인 기능이다.

여기서 새로운 요구사항으로 doSomething2라는 메소드를 만들고 그 메소드가 실행되는 시간을 측정해야 한다.
해당 요구사항을 만족시키기 위해서는 doSomething2 메소드를 만들고 timeCheck 메소드와 같이 시간을 측정하는 메소드를 또 작성하면 된다. 

하지만 이렇게 코드를 구성했을 때 문제점은 다음과 같다.

1. **N개의 메소드가 있을 때 N개의 시간측정 메소드가 필요하며, log 출력에서 log 내용을 바꿔야 한다면 N번 작업**해야 한다.
2. **비지니스 로직과 기능적인 역할을 하는 코드가 같은 Class 안에 혼재**된다.
3. **시간 측정 코드는 중복되는 부분이 더 많다.**
4. JAVA에서는 **다중 상속이 불가능**하기 때문에 한계가 있다.

이 때, 이런 코드를 개선할 수 있는 방법으로 디자인 패턴 중 하나인 [strategy 패턴](https://victorydntmd.tistory.com/292)을 사용할 수 있다. 
혹은 Spring의 핵심가치 중 하나인 AOP를 사용할 수 있다.
**AOP**는 '관점지향 프로그래밍'이다. **핵심 기능과 공통 기능을 분리하고, 공통 기능 코드를 재활용**하여 사용할 수 있도록 만들어주는 방법이다.

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbk6rsC%2FbtqE0ldZZzE%2FdtPP9ODdVlks606vpFsj01%2Fimg.png" height="400" width="600">
</p>

AOP를 이용하면 빨간 박스 안의 핵심 기능과 나머지 공통부분을 다른 Class로 뺄 수 있다. 때문에 AOP 기능을 **Cross-Cutting** 기능이라고도 한다.

### AOP 용어

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpfN5M%2FbtqE0lZkKfa%2FF6PvfwluAhiRRAs94EF0v0%2Fimg.png" height="350" width="500">
</p>

- **Aspect:** 기능적인 역할을 하는 모듈, 위의 예제에서 실제 비지니스 로직을 제외한 공통 기능 코드를 분리하여 재사용할 수 있도록 만든 모듈이다. Aspect는 Advice와 PointCut으로 이루어져 있다.

- **Advice:** Aspect의 기능 자체이다. Aspect를 공통 기능이라고 크게 묶었다면, Advice는 그 안의 세부적인, 주요 기능이다.

- **Joinpoint:** Advice가 적용될 수 있는 위치이다. Spring AOP에서 모든 메소드는 Join Point가 될 수 있다.

- **PointCut:** Advice가 적용될 Join Point를 선정하는 방법이다. 보통 특정 Join Point에 Advice를 적용하기 때문에 Join Point를 선정하는 방법이 필요하다.

- **Target:** Advice가 적용되어지는 기존 메소드, 클래스 등을 말한다.

- **Proxy:** Spring에서 AOP는 **Dynamic Proxy기법**으로 구현한다. 즉, AOP가 적용된 Target 메소드를 호출할 때 바로 그 메소드가 호출되는 것이 아니라 Advice가 
요청을 대신 받아주는 Wrapping 오브젝트가 호출되어 실행전에 전처리, 타겟 메소드 실행 후 후처리한다. (호출 및 처리 순서: 클라이언트 --> 프록시 --> 타깃)

- **Introduction:** AOP를 적용할 때 내부적으로 코드를 생성(Spring의 경우 wrapping class)하는 것을 말한다.

- **Weaving:** Aspect가 target에 적용되는 전체적인 과정을 말한다. 즉, PointCut으로 지정된 JoinPoint에 Advice가 적용되어 Target 호출 시 AOP Proxy가 만들어지는 과정이다.

---

## AOP 적용 타입

Spring AOP는 다음과 같은 type의 Advice를 제공한다.

- Advice의 동작 시점
| 동작시점 | 설명 |
|----------|--------|
| Before | 메소드 실행 전에 동작 |
| After | 메소드 실행 후에 동작 |
| After-returning | 메소드가 정상적으로 실행된 후에 동작 |
| After-throwing | 예외가 발생한 후에 동작 |
| Around | 메소드 호출 이전, 이후, 예외발생 등 모든 시점에서 동작 |

*AOP 구현방법 (추후)

