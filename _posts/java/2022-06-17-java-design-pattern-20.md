---
title:  "Design Pattern 2"
excerpt: ""
categories:
  - java
---
### Strategy Pattern 전략 패턴
- 행동 패턴
- 런타임에 어떤 알고리즘을 사용할지 선택
- 전략들을 쉽게 교체할수 있게 해줌
- '전략'이 포인트 (ex. 이메일을 어떻게 만드는가?)

```java
public class Chapter10S3 {
    public static void main(String args[]) {
        User user1 = User.builder(1, "Alice")
                .with(builder -> {
                    builder.emailAddress = "alice@test.co.kr";
                    builder.isVerified = false;
                    builder.friendUserIds = Arrays.asList(201, 202, 203, 204, 211, 212, 213, 214);
                }).build();
        User user2 = User.builder(2, "Bob")
                .with(builder -> {
                    builder.emailAddress = "bob@test.co.kr";
                    builder.isVerified = true;
                    builder.friendUserIds = Arrays.asList(212, 213, 214);
                }).build();
        User user3 = User.builder(3, "Charlie")
                .with(builder -> {
                    builder.emailAddress = "charlie@test.co.kr";
                    builder.isVerified = true;
                    builder.friendUserIds = Arrays.asList(201, 202, 203, 204, 211, 212);
                }).build();
        List<User> users = Arrays.asList(user1, user2, user3);

        EmailSender emailSender = new EmailSender();
        EmailProvider verifyYourEmailAdressEmailProvider = new VerifyYourEmailAdressEmailProvider();
        EmailProvider makeMoreFriendsEmailProvider = new MakeMoreFriendsEmailProvider();

        emailSender.setEmailProvider(verifyYourEmailAdressEmailProvider);
        users.stream()
                .filter(user -> !user.isVerified())
                .forEach(emailSender::sendEmail);

        emailSender.setEmailProvider(makeMoreFriendsEmailProvider);
        users.stream()
                .filter(User::isVerified)
                .filter(user -> user.getFriendUserIds().size() < 5)
                .forEach(emailSender::sendEmail);

        emailSender.setEmailProvider(user -> "'Play with Friends' email for " + user.getName());
        users.stream()
                .filter(User::isVerified)
                .filter(user -> user.getFriendUserIds().size() >= 5)
                .forEach(emailSender::sendEmail);
    }
}
```
```java
@FunctionalInterface
public interface EmailProvider {
    String getEmail (User user);
}
```

