---
title:  "Object"
excerpt: "Object Native Method"
categories: java
---
### Object Native Method
자바 최상위 클래스인 Object Class 에는 equals(), hashCode(), toString(), clone(), notify() 등 여러 
native method가 존재함.

#### getClass()
Object의 Class return
+ Class 클래스는 클래스와 인터페이스(Class, Interface, Enum, Annotation...)의 모든 정보를 담고있는 클래스이다.
+ 클래스 당 1개만 존재하며, 클래스 로더에 의해서 메모리에 올라갈 때 힙 영역에 자동으로 생성된다
+ 참고 : https://velog.io/@roro/Java-Object-%ED%81%B4%EB%9E%98%EC%8A%A4-getClass-%EA%B7%B8%EB%A6%AC%EA%B3%A0-Reflection-API
```java
@IntrinsicCandidate
public final native Class<?> getClass();
```
```java
System.out.println(order1.getClass()); // class yjjeon.example.chapter6.model.Order
```

#### hashCode()
+ 객체 해시코드란 객체를 식별하는 하나의 정수값
+ Object의 hashCode() 메서드는 객체의 메모리 번지를 이용해서 해시코드를 만들어 리턴하기 때문에 객체 마다 다른 값들을 가지고 있음.
+ 두 객체가 같은 객체인지 동일성을 비교

#### HashTable
contains() 메소드를 이용하여 탐색시 만약 List의 개수가 엄청나게 많다면 탐색할 때 상당히 오래걸림 O(n). 
이 때 HashTable을 사용하면 아주 효과적.
해시테이블은 hashCode() 메소드를 사용하여 주어진 키에 대한 해시 값을 계산하고 
내부적으로 이 값을 사용하여 데이터를 저장하기 때문에 접근할 때 훨씬 더 효율적
참고 : https://devlog-wjdrbs96.tistory.com/243

#### equals()
+ 함수 객체의 주소를 비교
+ String 의 equals 는 값이 같은지 비교. String 객체에서 재정의된 equals 사용
참고 : https://brunch.co.kr/@mystoryg/132

#### hashCode와 equals
[![alt](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdIKnZ4%2FbtrnTDIGf9n%2FkN705QfLfVVezteypMu2G0%2Fimg.png)](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdIKnZ4%2FbtrnTDIGf9n%2FkN705QfLfVVezteypMu2G0%2Fimg.png)
