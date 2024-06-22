Queue(큐)
==========
Queue(큐)의 사전적 의미는 '무엇을 기다리는 사람', '차량 등의 줄 혹은 줄을 서서 기다리는 것'을 의미하며 Stack과는 다르게 **먼저 집어 넣은 데이터가 먼저 나오는 FIFO(First In First Out)형태를 가지는 자료구조**

![queue.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/2f20a6c7-75a2-4e86-abcf-d206744c0856/queue.png)

- 데이터를 일시적으로 쌓아두기 위한 자료구조
- 입력과 출력을 한 쪽 끝(front, rear)으로 제한한다.
- 한 방향에서는 삽입 연산, 반대 방향에서는 삭제 연산이 이루어진다.
- 따라서 데이터를 순서대로 처리(순서를 보장)하고 관리할 때 매우 유용한 자료 구조이다.

**Queue 용어**

- `Front` / `Head` : 큐의 맨 앞에서 데이터를 삭제할 위치를 가리키는 포인터.
- `Rear` / `Tail` : 큐의 끝에 데이터를 삽입할 위치를 가리키는 포인터.
- `enQueue` : 큐의 ‘rear’ 위치에 원소를 삽입(추가)하는 연산
- `deQueue` : 큐의 ‘front’ 위치에 있는 원소를 삭제하고 반환하는 연산

**Queue의 사용법**

- Java에서 API로 Queue를 사용할 때, java.util.Queue는 인터페이스이며, 그 구현체로 java.util.LinkedList를 사용한다. 따라서 `Queue<String> queue = new LinkedList<String>()`로 선언해야 한다.

```java
import java.util.LinkedList;
import java.util.Queue;

public class QueueExample {
    public static void main(String[] args) {
        Queue<Integer> queue = new LinkedList<>();

        // add() 메서드: 큐의 끝에 요소를 추가하고, 큐가 가득 차면 예외가 발생한다.
        queue.**add**(10);

        // offer() 메서드: 큐의 끝에 요소를 추가하고, 큐가 가득 차면 false를 반환.
        queue.**offer**(40);

        // element() 메서드: 큐의 앞 요소 반환, (제거하지 않음)큐가 비어있으면 예외가 발생.
        queue.**element**();

        // peek() 메서드: 큐의 앞 요소 반환 (제거하지 않음), 큐가 비어있으면 null을 반환.
        queue.**peek**();

        // remove() 메서드: 큐의 앞 요소 제거 및 반환, 큐가 비어있으면 예외가 발생.
        queue.**remove**();
      
        // poll() 메서드: 큐의 앞 요소 제거 및 반환, 큐가 비어있으면 null을 반환.
        queue.**poll**();

        // isEmpty() 메서드: 큐가 비어 있는지 확인
        queue.**isEmpty**();

        // size() 메서드: 큐의 크기를 반환
        queue.**size**();
    }
}
```
