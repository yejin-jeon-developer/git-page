---
title:  "Design Pattern 1"
excerpt: ""
categories:
  - java
---
### Design Pattern
- 반복해서 등장하는 프로그래밍 문제들에 대한 해법들을 패턴화 해놓은 것
- 패턴들을 숙지해놓으면 비슷한 문제가 생겼을 때 패턴들이 이정표가 되어준다.

### Design Pattern 종류
1. 생성 패턴 (Creational Patterns) – 오브젝트의 생성에 관련된 패턴
2. 구조 패턴 (Structural Patterns) – 상속을 이용해 클래스/오브젝트를
조합하여 더 발전된 구조로 만드는 패턴
3. 행동 패턴 (Behavioral Patterns) – 필요한 작업을 여러 객체에
   분배하여 객체간 결합도를 줄이게 해주는 패턴

### Design Pattern & Functional Programming
1. 대부분의 디자인 패턴들은 구현에 많은 인터페이스/클래스/메서드를 필요로 한다
2. 함수형 프로그래밍을 이용해 몇몇 패턴을 좀 더 간단하게 구현할 수 있다.

### Builder Pattern 빌더 패턴
- Setter의 경우 의도치 않은 상황에 값이 변경될 수 있으며, 이를 완벽하게 컨트롤 할 수 없음.
- 값이 바뀌지 않길 바라는 값은 Setter 제거 후 Constructor를 통해서만 값 설정 -> immutable
- Default값 지정도 가능

###  Decorator Pattern 데코레이터 패턴
- 구조 패턴
- 객체에 기능을 계속 추가 (Decorate)
```java
public class Chapter10S2  {
    public static void main(String args[]) {
        Price unprocessedPrice = new Price("Original Price");

        PriceProcessor basicPriceProcessor = new BasicPriceProcessor();
        PriceProcessor discountPriceProcessor = new DiscountPriceProcessor();
        PriceProcessor taxPriceProcessor = new TaxPriceProcessor();

        PriceProcessor decoratedPriceProcessor = basicPriceProcessor
                .andThen(discountPriceProcessor)
                .andThen(taxPriceProcessor); // 원하는대로 processor를 추가하여 decoratedProcessor 생성
        // processor가 많아지면 굉장히 Class가 많아짐. -> 람다를 통해서 가능
        Price processedPrice = decoratedPriceProcessor.process(unprocessedPrice);
        System.out.println(processedPrice.getPrice());

        //바로 정의해서 추가하는것도 가능(람다), 하지만 이렇게 하면 재활용이 불가능하고 현재 스코프에서만 사용 가능
        //그렇기 때문에 이 패턴이 잘 쓰일만한지 판단하고 사용해야됨.
        PriceProcessor decoratedPriceProcessor2 = basicPriceProcessor
                .andThen(taxPriceProcessor)
                .andThen(price -> new Price(price.getPrice() + ", then apply another procedure"));
        Price processedPrice2 = decoratedPriceProcessor2.process(unprocessedPrice);
        System.out.println(processedPrice2.getPrice());
    }
}
```
```java
@FunctionalInterface
public interface PriceProcessor {
   Price process(Price price);

   default PriceProcessor andThen(PriceProcessor next) {
      return price -> next.process(process(price));
   }
}
```
```java
public class BasicPriceProcessor implements PriceProcessor {
   @Override
   public Price process(Price price) {
      return price;
   }
}
```
```java
public class DiscountPriceProcessor implements PriceProcessor {
   @Override
   public Price process(Price price) {
      return new Price(price.getPrice() + ", then applied discount");
   }
}
```

