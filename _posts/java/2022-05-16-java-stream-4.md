---
title:  "Method Reference"
excerpt: "Method Reference"
categories:
  - java
---
### Method Reference
- :: 을 사용
- 생략이 많기때문에 리턴타입과 매개변수 타입을 숙지

1. ClassName::staticMethodName
클래스의 정적메소드를 호출

```java
{
    int i = Integer.parseInt("1");
    System.out.println(i);
    Function<String, Integer> str2int = Integer::parseInt;
    int n = str2int.apply("2");
    System.out.println(n);
}
```

2. objectName::instanceMethodName
이미 선언된 객체의 InstanceMethod를 호출

```java
{
    String str = "Hello";
    Predicate<String> equalsToHello = str::equals;
    System.out.println(equalsToHello.test("Hello"));
    System.out.println(equalsToHello.test("Bye"));
}
```

3. ClassName::instanceMethodName

```java
    {
        Function<String, Integer> strLength = String::length;
        int length = strLength.apply("Hello world");
        System.out.println(length);
    
        BiPredicate<String, String> strEquals = String::equals;
        boolean isEqual = strEquals.test("hello", "hello");
        System.out.println(isEqual);
    
        List<User> users = new ArrayList<>();
        users.add(new User(1, "A"));
        users.add(new User(5, "B"));
        users.add(new User(3, "C"));
    
        printUserFields(users, user -> user.getId());
        printUserFields(users, User::getId);
        printUserFields(users, User::toString);
            
    }
    public static void printUserFields(List<User> users, Function<User, Object> getter) {
        for (User user : users) {
            System.out.println(getter.apply(user));
        }
    }
```
4. ClassName::new
클래스의 Constructor 호출

```java
public class Chapter5S3 {
    public static void main(String[] args) {
        //기존 방식은 if(sedan) new Sedan(); 이런 방식. 이런 방식으로 할 경우 차 종류가 많아지면 if/else문이 늘어
        Map<String, BiFunction<String, String, Car>> carTypeToConstructorMap = new HashMap<>();
        carTypeToConstructorMap.put("sedan", Sedan::new);
        carTypeToConstructorMap.put("van", Van::new);
        carTypeToConstructorMap.put("suv", Suv::new);

        String[][] inputs = new String[][] {
                {"sedan", "Sonata", "Hyundai"},
                {"van", "Sienna", "Toyota"},
                {"sedan", "Model S", "Tesla"},
                {"suv", "Sonata", "KIA"}
        };

        List<Car> cars = new ArrayList<>();

        for (int i = 0; i < inputs.length; i++) {
            String[] input = inputs[i];
            String carType = input[0];
            String name = input[1];
            String brand = input[2];

            cars.add(carTypeToConstructorMap.get(carType).apply(name, brand));
        }

        for (Car c : cars) {
            c.drive();
        }
    }
}
```


출력 결과


```
Driving a sedan name Sonata from Hyundai
Driving a van name Sienna from Toyota
Driving a sedan name Model S from Tesla
Driving a suv name Sonata from KIA

```

