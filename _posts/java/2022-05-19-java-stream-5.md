---
title:  "Java Stream"
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
만족하는 데이터만 걸러내는데 사용
Predicate에 true 를 반환하는 데이터만 존재하는 Stream 반환
```java
Stream<T> filter(Predicate<? super T> predicate);
```


