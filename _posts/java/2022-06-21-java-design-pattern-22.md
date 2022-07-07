---
title:  "Design Pattern 4"
excerpt: "Chain of Responsibility Pattern"
categories: java
---
### Chain of Responsibility Pattern
+ 행동 패턴
+ 처리 객체를 체인으로 엮 명령을 처리 객체들이 앞에서부터 하나씩 처리
+ 처리 할수 없을 경우 다음 체인으로 넘김
+ 체인의 끝에 다다르면 처리 종료
+ 새로운 처리객체를 추가하는 것으로 간단히 처리 객체 추가 가능


```java
public class OrderProcessStep {
    private final Consumer<Order> processOrder;
    private OrderProcessStep next;

    public OrderProcessStep(Consumer<Order> processOrder) {
        this.processOrder = processOrder;
    }

    public OrderProcessStep setNext(OrderProcessStep next) {
        if (this.next == null) {
            this.next = next;
        } else {
            this.next.setNext(next);
        }
        return this;
    }

    public void process(Order order) {
        processOrder.accept(order);
        Optional.ofNullable(next)
                .ifPresent(nextStep -> nextStep.process(order));
    }
}
```

```java
public class Chapter10S5 {
    public static void main(String[] args) {
        OrderProcessStep initializeStep = new OrderProcessStep(order -> {
            if (order.getStatus() == OrderStatus.CREATED) {
                System.out.println("Start processing order " + order.getId());
                order.setStatus(OrderStatus.IN_PROGRESS);
            }
        });
        OrderProcessStep setOrderAmountStep = new OrderProcessStep(order -> {
            if (order.getStatus() == OrderStatus.IN_PROGRESS) {
                System.out.println("Setting amount of order " + order.getId());
                order.setAmount(order.getOrderLines().stream().map(OrderLine::getAmount)
                        .reduce(BigDecimal.ZERO, BigDecimal::add));
            }
        });
        OrderProcessStep verifyOrderStep = new OrderProcessStep(order -> {
            if (order.getStatus() == OrderStatus.IN_PROGRESS) {
                System.out.println("Verifing order " + order.getId());
                if (order.getAmount().compareTo(BigDecimal.ZERO) <= 0) {
                    order.setStatus(OrderStatus.ERROR);
                }
            }
        });
        OrderProcessStep processPaymentStep = new OrderProcessStep(order -> {
            if (order.getStatus() == OrderStatus.IN_PROGRESS) {
                System.out.println("Processing payment of order " + order.getId());
                order.setStatus(OrderStatus.PROCESSED);
            }
        });
        OrderProcessStep handleErrorStep = new OrderProcessStep(order -> {
            if (order.getStatus() == OrderStatus.ERROR) {
                System.out.println("Send out 'Failed to process order' alert for order " + order.getId());
            }
        });
        OrderProcessStep completeProcessingOrderStep = new OrderProcessStep(order -> {
            if(order.getStatus() == OrderStatus.PROCESSED) {
                System.out.println("Complete order for " + order.getId());
            }
        });

        OrderProcessStep chainedOrderProcessSteps = initializeStep
                .setNext(setOrderAmountStep)
                .setNext(verifyOrderStep)
                .setNext(processPaymentStep)
                .setNext(handleErrorStep)
                .setNext(completeProcessingOrderStep);

        Order order = new Order()
                .setId(1001L)
                .setStatus(OrderStatus.CREATED)
                .setOrderLines(Arrays.asList(
                        new OrderLine().setAmount(BigDecimal.valueOf(1000)),
                        new OrderLine().setAmount(BigDecimal.valueOf(2000))));
        chainedOrderProcessSteps.process(order);

        Order failingOrder = new Order()
                .setId(1002L)
                .setStatus(OrderStatus.CREATED)
                .setOrderLines(Arrays.asList(
                        new OrderLine().setAmount(BigDecimal.valueOf(1000)),
                        new OrderLine().setAmount(BigDecimal.valueOf(-2000))));
        chainedOrderProcessSteps.process(failingOrder);
    }
}
```
출력 결과
```
Start processing order 1001
Setting amount of order 1001
Verifing order 1001
Processing payment of order 1001
Complete order for 1001
Start processing order 1002
Setting amount of order 1002
Verifing order 1002
Send out 'Failed to process order' alert for order 1002
```