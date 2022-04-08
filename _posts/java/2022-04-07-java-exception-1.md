---
title:  "ConcurrentModificationException"
excerpt: "Java ConcurrentModificationException 발생 이유 및 해결 방법"
categories:
  - java
---
## ConcurrentModificationException
for each 문에서 ArrayList 내 객체 remove시 발생함
1. Object remove 시 fastRemove 함수가 실행되며 modCount 가 증가됨. 이후 순회시 expectedModCount와 modCount가 불일치 하여 Exception 발생
2. 테스트시 오류가 발생하지 않은 케이스도 있었는데, 리스트의 마지막 객체를 삭제할 경우 이후 modCount가 증가하여도 순회가 종료되어 Exception 발생하지 않음.  

```java
public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable {
   int expectedModCount = modCount;

   public E next() {
      checkForComodification();
      int i = cursor;
      if (i >= size)
         throw new NoSuchElementException();
      Object[] elementData = ArrayList.this.elementData;
      if (i >= elementData.length)
         throw new ConcurrentModificationException();
      cursor = i + 1;
      return (E) elementData[lastRet = i];
   }
   
   final void checkForComodification() {
      if (modCount != expectedModCount)
         throw new ConcurrentModificationException();
   }
   
   public boolean remove(Object o) {
      final Object[] es = elementData;
      final int size = this.size;
      //...
      fastRemove(es, i);
      return true;
   }

   private void fastRemove(Object[] es, int i) {
      modCount++;
      final int newSize;
      if ((newSize = size - 1) > i)
         System.arraycopy(es, i + 1, es, i, newSize - i);
      es[size = newSize] = null;
   }
}
```

Java8 removeIf 사용하여 Exception 발생 막음

# Java8 removeIf()
오류 발생 소스
```java
    for (MemberCardVO vo : memberCardList) {
        if (MASTER_CARD_CODE.equals(vo.getCardBrndCd())) {
           memberCardList.remove(vo);
        }
    }
```
수정 소스
```java
   memberCardList.removeIf(memberCardVO -> MASTER_CARD_CODE.equals(memberCardVO.getCardBrndCd()));
```


