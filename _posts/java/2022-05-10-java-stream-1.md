---
title:  "함수형 프로그래밍"
excerpt: "함수형 프로그래밍 1"
categories:
  - java
---
### 함수형 프로그래밍
- 명령형 프로그래밍(How to do) vs 선언형 프로그래밍(What to do)
- 함수가 1급시민
* 매개변수, 리턴값, 변수에 담을수 있어야함.
- 함수를 Object 형식으로 표현하면 가능 (Java8 부터 지원->Funtional Interface)

### Funtional Interface
java.util.function

### 함수의 구성요소
함수 이름, 리턴타입, 반환타입, 함수 내용(body)

### Lamda Expression
이름이 없는 함수
```java
public class Main {
    public static void main(String[] args) {
        // 1. Function<Integer, Integer> myAdder = new Adder();
        /* 2. Lamda Expression
            Function<Integer, Integer> myAdder = (Integer x) -> {
            return x + 5;
        };
         */
        // 3. 추가 생략 가능
        Function<Integer, Integer> myAdder = x -> x + 5; // 매개변수 유추가능(괄호생략), 리턴타입 유추가능 (중괄호, return 생략가능)

        System.out.println(myAdder.apply(10));
    }
}
```
### BiFunction Interface
매개변수가 두개일때.
세개일때는 제공X , 직접 만들어야됨.

### @FunctionalInterface
단 하나의 abstract method 만 가지고 있음. (Single Abstract Method)
static, default 메소드는 이미 구현되어 있음.
```java

@FunctionalInterface
public interface TriFunction<T, U, A, R> {
    R apply(T t, U u, A a);
}

public class Main {
    public static void main(String[] args) {
        TriFunction<Integer, Integer, Integer, Integer> triAdder = (x,y,z) -> x+y+z;

        int result2 = triAdder.apply(1,2,3);
        System.out.println(result2);

    }
}
```


