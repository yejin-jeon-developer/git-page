---
title:  "Java Stream 3 - 구성요소"
excerpt: "Stream의 구성요소"
categories:
  - java
---
### Stream의 구성요소
- Stream Pipe Line
- 소스(컬렉션, 배열) -> 중간처리(0개 이상의 filter, map) -> 종결처리(Collect, reduce)

```java
public class Chapter6S4 {
    public static void main(String[] args) {
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
                .setVerified(false)
                .setEmailAddress("Charlie@naver.com");
        List<User> users = Arrays.asList(user1, user2, user3);

        //명령형 프로그래밍 방식(How to do), Nested Code가 존재함
        List<String> emailList = new ArrayList<>();
        for (User user : users) {
            if (!user.isVerified()) {
                emailList.add(user.getEmailAddress());
            }
        }
        System.out.println(emailList);

        //선언형 프로그래밍(What to do : filtering, mapping), 각 과정에서 무엇을 해야되는지.
        List<String> unVerifiedEmailAdresses = users.stream()
                .filter(user -> !user.isVerified())
                .map(User::getEmailAddress)
                .collect(Collectors.toList());

        System.out.println(unVerifiedEmailAdresses);

        LocalDateTime now = LocalDateTime.now(ZoneId.of("Asia/Seoul"));
        Order order1 = new Order()
                .setId(1001)
                .setStatus(Order.OrderStatus.CREATED)
                .setCreatedByUserId(101)
                .setCreatedAt(now.minusHours(4));
        Order order2 = new Order()
                .setId(1002)
                .setStatus(Order.OrderStatus.ERROR)
                .setCreatedByUserId(103)
                .setCreatedAt(now.minusHours(1));
        Order order3 = new Order()
                .setId(1003)
                .setStatus(Order.OrderStatus.ERROR)
                .setCreatedByUserId(102)
                .setCreatedAt(now.minusHours(36));
        Order order4 = new Order()
                .setId(1004)
                .setStatus(Order.OrderStatus.ERROR)
                .setCreatedByUserId(104)
                .setCreatedAt(now.minusHours(15));
        Order order5 = new Order()
                .setId(1005)
                .setStatus(Order.OrderStatus.IN_PROGRESS)
                .setCreatedByUserId(101)
                .setCreatedAt(now.minusHours(10));
        List<Order> orders = Arrays.asList(order1, order2, order3, order4, order5);

        //error상태이며, UserId를 추출해서 List에
        List<Long> errorUsers = orders.stream()
                .filter(order -> order.getStatus() == Order.OrderStatus.ERROR)
                .map(Order::getCreatedByUserId)
                .collect(Collectors.toList());

        System.out.println(errorUsers);

        //error 오더 중에서 만든지 24시간 이내인
        //now.isAfter() isBefore()
        List<Order> filteredList = orders.stream()
                .filter(order -> order.getStatus() == Order.OrderStatus.ERROR)
                .filter(order -> order.getCreatedAt().isAfter(now.minusHours(24)))
                .collect(Collectors.toList());
        System.out.println(filteredList);
    }
}
```