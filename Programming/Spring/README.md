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

