---
title:  "Java Stream 1"
excerpt: "Stream"
categories:
  - java
---
### Stream
- 데이터의 흐름
- Collection 형태의 데이터를 람다를 이용해 간결하고 직관적으로 프로세스 해줌
- 기존 loop 대체
- 손쉽게 병렬 처리

```java
public class Chapter6S1 {
    public static void main(String[] args) {
        Stream<String> nameStream = Stream.of("A", "B", "C");
        List<String> names = nameStream.collect(Collectors.toList());
        System.out.println(names);

        String[] cityArray = new String[] {"San Jose", "Seoul", "Tokyo"};
        Stream<String> cityStream = Arrays.stream(cityArray);
        List<String> cityList = cityStream.collect(Collectors.toList());
        System.out.println(cityList);

        Set<Integer> numberSet = new HashSet<>(Arrays.asList(3, 5, 7));
        Stream<Integer> numberStream = numberSet.stream();
        List<Integer> numberList = numberStream.collect(Collectors.toList());
        System.out.println(numberList);
    }
}

```
출력 결과
```
[A, B, C]
[San Jose, Seoul, Tokyo]
[3, 5, 7]
```

### Filter
+ 만족하는 데이터만 걸러내는데 사용
+ Predicate에 true 를 반환하는 데이터만 존재하는 Stream 반환

```java
Stream<T> filter(Predicate<? super T> predicate);
```

```java
public class Chapter6S2 {
    public static void main(String[] args) {
        Stream<Integer> numberStream = Stream.of(3, -5, 7, 10, -3);
        Stream<Integer> filteredNumberStream = numberStream.filter(x -> x > 0);

        List<Integer> filteredNumbers = filteredNumberStream.collect(Collectors.toList());
        System.out.println(filteredNumbers);

        Stream<Integer> newFilteredNumberStream = Stream.of(3, -5, 7, 10, -3)
                .filter(x -> x > 0);

        // 최종 형태
        List<Integer> newFlteredNumbers =  Stream.of(3, -5, 7, 10, -3)
                .filter(x -> x > 0)
                .collect(Collectors.toList());
        System.out.println(newFlteredNumbers);

        User user1 = new User()
                .setId(101)
                .setName("Ailce")
                .setVerified(true)
                .setEmailAddress("Ailce@naver.com");
        User user2 = new User()
                .setId(102)
                .setName("Bob")
                .setVerified(false)
                .setEmailAddress("Bob@naver.com");
        User user3 = new User()
                .setId(103)
                .setName("Charlie")
                .setVerified(true)
                .setEmailAddress("Charlie@naver.com");

        List<User> users = Arrays.asList(user1, user2, user3);
        List<User> verifiedUsers = users.stream()
                .filter(User::isVerified)
                .collect(Collectors.toList());
        System.out.println(verifiedUsers);

        List<User> unVerifiedUsers = users.stream()
                .filter(user -> !user.isVerified())
                .collect(Collectors.toList());
        System.out.println(unVerifiedUsers);

        Order order1 = new Order()
                .setId(1001)
                .setStatus(Order.OrderStatus.CREATED);
        Order order2 = new Order()
                .setId(1002)
                .setStatus(Order.OrderStatus.ERROR);
        Order order3 = new Order()
                .setId(1003)
                .setStatus(Order.OrderStatus.PROCESSED);
        Order order4 = new Order()
                .setId(1004)
                .setStatus(Order.OrderStatus.ERROR);
        Order order5 = new Order()
                .setId(1005)
                .setStatus(Order.OrderStatus.IN_PROGRESS);

        List<Order> orders = Arrays.asList(order1, order2, order3, order4, order5);
        //filter orders in error state
        List<Order> errorOrders = orders.stream()
                .filter(order -> order.getStatus() == Order.OrderStatus.ERROR)
                .collect(Collectors.toList());
        System.out.println(errorOrders);
    }
}
```



