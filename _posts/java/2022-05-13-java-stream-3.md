---
title:  "Java Functional Interface 2 : Predicate, Comparator"
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
Collections.sort 사용시 Comparator를 넘겨줘서 sorting 가능
```java
  public static <T> void sort(List<T> list, Comparator<? super T> c) {
        list.sort(c);
        }
```
```java
  public class Study {
    public static void main(String[] args) {
        List<User> userList = new ArrayList<>();
        userList.add(new User(3, "A"));
        userList.add(new User(1, "B"));
        userList.add(new User(5, "C"));
        System.out.println(userList);

        // ID 순서로 sort해보자
        Comparator<User> idComparator = (u1, u2) -> u1.getId() - u2.getId();
        Collections.sort(userList, idComparator);
        System.out.println(userList);

        // Name 순으로 Sort
        Collections.sort(userList, (u1, u2) -> u1.getName().compareTo(u2.getName()));
        System.out.println(userList);
    }
}
```

출력결과
```
[User{id=3, name='A'}, User{id=1, name='B'}, User{id=5, name='C'}]
[User{id=1, name='B'}, User{id=3, name='A'}, User{id=5, name='C'}]
[User{id=3, name='A'}, User{id=1, name='B'}, User{id=5, name='C'}]
```
