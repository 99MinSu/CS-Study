# 벡터(Vector)

## 벡터(Vector)란?

`Vector`은 동적 배열(dynamic array)로, 크기가 가변적으로 변할 수 있는 배열을 의미한다. 요소를 추가할 때 필요에 따라 크기를 자동으로 확장합니다. 

- 자바에서는 컬렉션 프레임워크가 발전하면서 `Vector` 보다는  `ArrayList`와 같은 다른 컬렉션이 더 많이 사용한다.

### 주요 특징

1. **동적 크기 조절**: 요소가 추가되면 자동으로 크기가 조절됩니다.
2. **동기화**: 모든 메서드가 동기화되어 멀티스레드 환경에서 안전합니다.(스레드 세이프)
3. **배열 기반**: 내부적으로 배열을 사용하여 요소를 저장합니다.

## 벡터(Vector) 사용법

```java
import java.util.Vector;

public class VectorExample {
    public static void main(String[] args) {
        Vector<Integer> vector = new Vector<>();

        // 요소 추가
        vector.add(1);
        vector.add(2);
        vector.add(3);

        // 요소 접근
        System.out.println("First element: " + vector.get(0));
        System.out.println("Second element: " + vector.get(1));

        // 요소 제거
        vector.remove(1); // 두 번째 요소 제거

        // 크기 및 용량 확인
        System.out.println("Size: " + vector.size());
        System.out.println("Capacity: " + vector.capacity()); (ArrayList에서는 불가능)

        // 요소 순회
        for (Integer i : vector) {
            System.out.println("Element: " + i);
        }
        v.clear(); // 요소만 제거
				v.removeAllElements(); // 요소도 제거하고 용량도 0으로 만듬
    }
}
```

- ArrayList와 다른 메서드가 보이는데removeAllElements() 는clear() 메서드와 달이 모든 요소를 지우고 용량(capacity)도 0으로 만든다.

## **ArrayList Vs Vector**

Vector은 ArrayList와 같이 List 인터페이스를 상속받는 컬렉션 프레임워크로 Vector는 ArrayList와 기능 상 거의 동일하다. 메서드 구성도 거의 같다. 하지만 한 가지 다른 점이 있는데 바로 **메서드에 synchronized 키워드 유무이다.** 

- Vector 클래스를 보면 모든 메서드에 synchronized 키워드가 걸려있음을 볼 수 있다.

![img1 daumcdn](https://github.com/99MinSu/CS-Study/assets/89891488/04800172-db1f-4f9a-b421-6df2590cf879)

- synchronized 키워드는 멀티 쓰레드 환경에서 두개 이상의 쓰레드가 하나의 변수에 동시에 접근을 할 때 Race condition(경쟁상태)이 발생하지 않도록 한다.

따라서 Vector 클래스는 멀티 쓰레드 환경에서 안전하게 사용할 수 있는 컬렉션이라고 한다.  하지만 반대로 synchronized 키워드 때문에 프로그램 성능이 떨어질 수도 있다는 문제점이 있다.

- Race condition(경쟁상태)를 따지지 않아도 되는 환경에서도 메서드를 실행하면 동기화 여부를 따지느라 **일반적인 메서드보다 속도가 느려질 수 있다.**(Overhead)

Vector 클래스의 메소드에 대해서는 synchronized 처리가 되어있지만, **Vector 인스턴스 자체에 대해서는 동기화 처리가 되어있지 않기** 때문에 동시 엑세스에 한해서 여전히 쓰레드에 안전하지 않다. 

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Vector<Integer> vec = new Vector<>();

        new Thread(() -> {
            synchronized (vec) { // vec 객체 자체를 동기화 처리함
                vec.add(1);
                vec.add(2);
                vec.add(3);
                System.out.println(vec.get(0));
                System.out.println(vec.get(1));
                System.out.println(vec.get(2));
            }
        }).start();

        new Thread(() -> {
            synchronized (vec) { // vec 객체 자체를 동기화 처리함
                vec.remove(0);
                vec.remove(0);
                vec.remove(0);
            }
        }).start();

        // 출력
        new Thread(() -> {
            try {
                Thread.sleep(1000); // 쓰레드가 다 돌때까지 1초 대기

                System.out.println("Vector size : " + vec.size());
            } catch (InterruptedException ignored) {}
        }).start();
    }
}
```

싱글 쓰레드 환경에서는 동기화가 붙어 있어 느린 Vector를 쓸 이유가 없고, 멀티 쓰레드 환경에서도 쓰레드에 안전하지 않기 때문에 Vector를 쓸 이유가 없다.

| 특징 | Vector | ArrayList |
| --- | --- | --- |
| 동기화 여부 | 예 (Thread-safe) | 아니오 (Not thread-safe) |
| 성능 | 단일 스레드 환경에서 성능 저하 발생 | 단일 스레드 환경에서 더 나은 성능 |
| 기본 크기 증가 방식 | 최대 인덱스 초과 시 현재 배열 크기의 100% 증가 | 최대 인덱스 초과 시 현재 배열 크기의 50% 증가 |

 `Vector`는 동기화된 메서드로 인해 **단일 스레드 환경에서 성능이 저하되기 때문에 사용을 지양**한다. 멀티 스레드 환경에서도  Collections 클래스에서 제공하는 synchronizedList() 메서드를 통해 ArrayList 뿐만 아니라 LinkedList 및 다른 컬렉션 역시 자료구조의 특성을 유지하면서도 동기화 처리가 된 컬렉션들을 만들어주기 때문에 **사용이 지양 된다.**
