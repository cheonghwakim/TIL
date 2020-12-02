# 1주차
 
 * [Java와 C의 차이점](#Java와-C의-차이점)
 * [객체지향 언어의 특징](#객체지향-언어의-특징)
  * [추상화](#IoC의-구성요소-DI와-DL)
  * [캡슐화](#IoC의-구성요소-DI와-DL)
  * [상속](#IoC의-구성요소-DI와-DL)
* [String, StringBuilder, StringBuffer 차이점](#String,-StringBuilder,-StringBuffer-차이점)
* [Overloading과 Overriding 차이점](#Overloading과-Overriding-차이점)
* [컬렉션 자료구조 종류와 특징](#컬렉션-자료구조-종류와-특징)
  * [1. Set](#1.-Set)
  * [2. List](#2.-List)
  * [3. Queue](#3.-Queue)
  * [4. Map](#4.-Map)
* [쓰레드의 장점/단점](#쓰레드의-장점/단점)
* [쓰레드 사용 시 주의할 점](#쓰레드-사용-시-주의할-점)
* [쓰레드 사용 여부 결정 요소](#쓰레드-사용-여부-결정-요소)


## Java와 C의 차이점




## 객체지향 언어의 특징


## [String, StringBuilder, StringBuffer 차이점](https://github.com/cheonghwakim/CS-STUDY/tree/main/JAVA#String,-StirngBuffer,-StringBuilder%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)



## Collection 자료구조 종류와 특징

**Collection은 데이터의 집합, 그룹을 의미한다.** JCF(Java Collections Framework)는 이러한 데이터, 자료구조인 컬렉션과 이를 구현하는 클래스를 정의하는 인터페이스를 제공한다. 아래의 사진은 Java 컬렉션 프레임워크의 상속 구조를 나타낸다.

<p align="center">
  <img src="https://blog.kakaocdn.net/dn/I1jdr/btqDACgkEMb/VwcO1xEQWKVDiH5NQFAyp1/img.png" height="450" width="550">
</p>

Collection 인터페이스는 또, **List, Set, Queue로 크게 3가지 인터페이스**로 분류된다. Map의 경우 Collection 인터페이스를 상속받고 있지 않지만 Collection으로 분류된다. 

### 1. Set

Set은 **원소 간에 순서가 없고, 중복 값을 허용하지 않는다.**
자바에서는 **HashSet, TreeSet, LinkedList**의 3가지 구현체가 있다.
- HashSet은 해쉬 테이블에 원소를 저장하여 성능 면에서 가장 우수하다.
- TreeSet은 [레드-블랙 트리](https://itstory.tk/entry/%EB%A0%88%EB%93%9C%EB%B8%94%EB%9E%99-%ED%8A%B8%EB%A6%ACRed-black-tree)에 원소를 저장해서, 값에 따라 순서가 결정되지만 HashSet보다는 성능이 느리다.
- **LinkedHashSet은 HashSet의 문제점인 순서의 불명확성의 단점을 제거한 구체이다.**

### 2. List

List는 배열처럼 **순서를 가지는 원소들의 모임으로 중복 값을 가질 수 있는 자료구조**이다.
종류는 **ArrayList, LinkedList, Vector**가 있다.

- ArrayList는 단방향 포인터 구조로 각 데이터에 대한 인덱스를 가지고 있어 조회 기능에 성능이 뛰어나다. 또, 저장되는 데이터의 개수에 따라 크기가 유동적으로 변하기 때문에 초기에 크기를 정해줘야 하는 배열보다 편리하다.
- LinkedList는 **양방향 포인터 구조로 데이터의 삽입, 삭제가 빈번할 경우** 데이터의 위치정보만 수정하면 되기 때문에 유용하다. 스택, 큐, 데큐 등을 만들기 위한 용도로 쓰인다.
- Vector는 과거에 대용량 처리를 위해 사용되었다. 내부에서 자동으로 동기화처리가 일어나 비교적 성능이 좋지않고 무거워서 잘 쓰이지 않는다.

  * 즉, 인덱스를 가지고 원소를 접근하는 연산은 ArrayList의 성능이 더 좋고, 중간에 원소의 삽입 삭제가 빈번히 일어나는 경우에는 LinkedList의 성능이 더 좋다. 
  
  * 배열을 리스트로 변경하기
  ``` java
  List<String> list = Arrays.asList(new String[5]);
  ```
### 3. Queue

Queue는 데이터를 처리하기 전에 잠시 저장하고 있는 **선입선출**의 자료구조이다. tail에서 원소를 추가하고, head에서 원소를 삭제한다. 

### 4. Map

Map 자체는 Collection 인터페이스와 별개이지만, json의 형식과 유사한 Key-Value 자료구조로 자주 쓰인다. Dictionary와 같은 자료 구조로, 중복된 키를 가질 수 없고 각 키는 오직 하나의 값에만 매핑될 수 있다. Map의 종류에는 **HashMap, TreeMap, LinkedHashMap** 등이 있다.
- HashMap은 중복과 순서가 허용되지 않으며 null 값이 올 수 있다. 
- TreeMap은 정렬된 순서대로 키(Key)와 값(Value)를 저장하여 검색이 빠르다.
- HashTable은 HashMap보다는 느리지만 동기화가 지원된다. null 값이 올 수 없다.

* HashMap은 해싱 테이블에 데이터를 저장하고 TreeMap은 탐색 트리에 저장한다. 
  * 키들을 **정렬된 순서로 방문할 필요가 없다면 HashMap이 약간 빠르다.**




### Collection 인터페이스의 특징

| 인터페이스 | 구현 클래스 | 특징 |
|------------|-----------|-------|
| Set | HashSet, TreeSet, LinkedHashSet, AbstractSet | 중복 데이터 불허, 입력시 순서 무시, 순차적인 접근 위해 Iterator 사용 |
| List | ArrayList, LinkedList, Vector, AbstractList | 데이터 중복 가능, 수집의 순서 있음, Vector는 동기화/ArrayList는 동기화 X |
| Queue | LinkedList, PriorityQueue | List와 유사 |
| Map | HashMap, Hashtable, TreeMap, AbstractMap, Attribute, IdentityHashMap, RenderingHints, WeakHashMap | 키(Key)-값(Value)의 쌍으로 이루어진 데이터의 집합, 순서는 유지되지 X, 키(Key)의 중복 허용 X & 값(Value)의 중복 허용 O, 많은 양의 데이터에서 원하는 특정 데이터에 접근(검색)할 때 사용 |
