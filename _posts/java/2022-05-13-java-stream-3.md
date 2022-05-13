---
title:  "Java Functional Interface 2"
excerpt: "Predicate, Comparator"
categories:
  - java
---
### Predicate
True or False
```java
@FunctionalInterface
public interface Predicate<T> {

    boolean test(T t);
    
    // 다른 Predicate을 둘다 만족하는지
    default Predicate<T> and(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) && other.test(t);
    }
    
    // 만든 Predicate 과 반대의 Predicate 리턴
    default Predicate<T> negate() {
        return (t) -> !test(t);
    }


    // 다른 Predicate과 둘중 하나 만족하는지 여부
    default Predicate<T> or(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) || other.test(t);
    }
}
```

### Primtive type이 포함된 Functional Interface
ex)IntConsumer, DoublePredicate...
- Consumer, Predicate 등 구현시 Wrapper 타입을 사용하게 되는데 (Integer, Double..)
Primitive로 구현된 인터페이스 사용시 메모리 효율적으로 이용 가능

### Comparator
```java
@FunctionalInterface
public interface Comparator<T> {
    int compare(T o1, T o2);
    // o1 < o2 음수 리턴
    // o1 == o2 0 리턴
    // o1 > o2 양수 리턴
}
```
