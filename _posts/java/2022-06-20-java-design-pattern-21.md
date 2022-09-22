---
title:  "Design Pattern 3 - Template Method Pattern"
excerpt: "Template Method Pattern"
categories:
  - java
---
### Template Method Pattern
+ 행동 패턴
+ 상위클래스는 Template만 제공. 하위클래스에서 내용 정의
+ 큰 뼈대를 따라서 실행하고 세부 내용은 달라짐

```java
public class Chapter10S4 {
    public static void main(String args[]) {
        User user1 = User.builder(1, "Alice")
                .with(builder -> {
                    builder.emailAddress = "alice@test.co.kr";
                    builder.isVerified = false;
                    builder.friendUserIds = Arrays.asList(201, 202, 203, 204, 211, 212, 213, 214);
                }).build();

        UserService userService = new UserService();
        InternalUserService internalUserService = new InternalUserService();

        userService.createUser(user1);
        internalUserService.createUser(user1);

        UserServiceInFunctionalWay userServiceInFunctionalWay
                = new UserServiceInFunctionalWay(user -> {
                        System.out.println("Validating User in functional way");
                        return user.getEmailAddress().isPresent() && user.getName() != null;
                    },
                    user -> System.out.println("Write user " + user.getName() + " to DB"));

        userServiceInFunctionalWay.createUser(user1);
    }
}
```
```java
public class UserServiceInFunctionalWay {
    private final Predicate<User> validateUser;
    private final Consumer<User> writeToDB;

    public UserServiceInFunctionalWay(Predicate<User> validateUser, Consumer<User> writeToDB) {
         this.validateUser = validateUser;
         this.writeToDB = writeToDB;
    }

    public void createUser(User user) {
        if (validateUser.test(user)) {
            writeToDB.accept(user);
        } else {
            System.out.println("Cannot create user");
        }
    }
}
```