---
title:  "Java Functional Interface 1"
excerpt: "Supplier, Consumer, BiConsumer"
categories:
  - java
---
### Supplier
```java
@FunctionalInterface
public interface Supplier<T> {

    /**
     * Gets a result.
     *
     * @return a result
     */
    T get();
}
```

함수를 넘겨줘서 printRandomDouble에서 사용 (1등 시민 조건 - 함수를 파라미터값으로 이용)
```java
public class Main {
    public static void main(String[] args) {
        Supplier<Double> doubleSupplier = () -> Math.random(); // 함수를 Object화 
        printRandomDouble(doubleSupplier, 5);
    }

    public static void printRandomDouble(Supplier<Double> randomSupplier, int count) {
        for (int i = 0; i < count; i++) {
            System.out.println(randomSupplier.get());
        }
    }
}
```

### Consumer
리턴없이 소비만 함
```java
@FunctionalInterface
public interface Consumer<T> {
    void accept(T t);

    default Consumer<T> andThen(Consumer<? super T> after) {
        Objects.requireNonNull(after);
        return (T t) -> { accept(t); after.accept(t); };
    }
}
```

제네릭 사용하여 여러 타입을 process 하도록 더 유연하게 구현 가능
```java
public class Main {
    public static void main(String[] args) {
        List<Integer> inputs = Arrays.asList(4, 2, 3); //immutable add하면 에러남
        Consumer<Integer> processor = (x) -> System.out.println("Processing Integer : " + x);
        process(inputs, processor);
        Consumer<Integer> diffProcessor = (x) -> System.out.println("Processing Integer in diff way : " + x);
        process(inputs, diffProcessor);

        List<Double> doubleInputs = Arrays.asList(1.1, 2.2, 3.3);
        Consumer<Double> doubleProcessor = (x) -> System.out.println("Processing Double : " + x);
        process2(doubleInputs, doubleProcessor );
    }

    // processor를 넘겨줘서 다양한 방법으로 process 가능
    public static void process(List<Integer> inputs, Consumer<Integer> processor) {
        for (Integer i : inputs) {
            processor.accept(i);
        }
    }

    public static <T> void process2(List<T> inputs, Consumer<T> processor) {
        for (T t : inputs) {
            processor.accept(t);
        }
    }
}
```

### BiConsumer
```java
@FunctionalInterface
public interface BiConsumer<T, U> {

    void accept(T t, U u);
    
}
```
```java
public class Main {
    public static void main(String[] args) {
        List<Double> doubleInputs = Arrays.asList(1.1, 2.2, 3.3);
        BiConsumer<Integer, Double> myProcessor = (index, input)
                -> System.out.println("Processing " + input + " at index  " + index );
        process3(doubleInputs, myProcessor);
    }

    public static <T> void process3 (List<T> inputs, BiConsumer<Integer, T> processor) {
        for (int i = 0; i < inputs.size(); i++) {
            processor.accept(i, inputs.get(i));
        }
    }
}
```




