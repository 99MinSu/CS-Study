Heap & Priority Queue
--
## 힙(heap)

- 완전 이진 트리의 일종으로 우선순위 큐를 위하여 만들어진 자료구조이다.
- 여러 개의 값들 중에서 최댓값이나 최솟값을 빠르게 찾아내도록 만들어진 자료구조이다.
- 힙은 일종의 **반정렬 상태**(**느슨한 정렬 상태**) 를 유지한다.
    - 큰 값이 상위 레벨에 있고 작은 값이 하위 레벨에 있다는 정도
    - 간단히 말하면 부모 노드의 키 값이 자식 노드의 키 값보다 항상 큰(작은) 이진 트리를 말한다.
    - 힙 트리에서는 중복된 값을 허용한다. (이진 탐색 트리에서는 중복된 값을 허용하지 않는다.)

## 힙(heap)의 종류

**최대 힙(max heap)**

- 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리
    - key(부모 노드) >= key(자식 노드)

**최소 힙(min heap)**

- 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리
    - key(부모 노드) <= key(자식 노드)

![image](https://github.com/Minsu17/CS-Study/assets/89891511/05111a30-e67d-48e2-9fc3-bba57cab031f)


## 힙(heap)의 삽입

1. 힙에 새로운 요소가 들어오면, 일단 새로운 노드를 힙의 마지막 노드에 이어서 삽입한다.
2. 새로운 노드를 부모 노드들과 교환해서 힙의 성질을 만족시킨다.
- 아래의 최대 힙(max heap)에 새로운 요소 8을 삽입해보자.
    
    ![maxheap-insertion](https://github.com/Minsu17/CS-Study/assets/89891511/458557bc-4475-4a62-bbf9-32e4c331762e)

    
    ## 힙(heap)의 삭제
    
    1. 최대 힙에서 최댓값은 루트 노드이므로 루트 노드가 삭제된다.
        - 최대 힙(max heap)에서 삭제 연산은 최댓값을 가진 요소를 삭제하는 것이다.
    2. 삭제된 루트 노드에는 힙의 마지막 노드를 가져온다.
    3. 힙을 재구성한다.
        
        ![maxheap-delete](https://github.com/Minsu17/CS-Study/assets/89891511/654436d2-8a17-4a8d-841a-42d6a5d42c91)

        
        ## 힙(heap)의 구현
        
        ### 최대 힙
        
        ```java
        import java.util.PriorityQueue;
        import java.util.Collections;
        
        public class MaxHeap {
            public static void main(String[] args) {
                PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
        
                maxHeap.add(10);
                maxHeap.add(5);
                maxHeap.add(20);
        
                System.out.println("Max Heap:");
                while (!maxHeap.isEmpty()) {
                    System.out.println(maxHeap.poll());
                }
            }
        }
        ```
        
        출력결과
        
        ```mathematica
        Max Heap:
        20
        10
        5
        ```
        
        ### 최소 힙
        
        ```java
        import java.util.PriorityQueue;
        
        public class MinHeap {
            public static void main(String[] args) {
                PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        
                minHeap.add(10);
                minHeap.add(5);
                minHeap.add(20);
        
                System.out.println("Min Heap:");
                while (!minHeap.isEmpty()) {
                    System.out.println(minHeap.poll());
                }
            }
        }
        ```
        
        출력결과
        
        ```mathematica
        Min Heap:
        5
        10
        20
        ```
        

## 우선순위 큐(Priority Queue)

큐(Queue)는 먼저 들어오는 데이터가 먼저 나가는 **FIFO(First In First Out)** 형식의 자료구조이다.

우선순위 큐(Priority Queue)는 먼저 들어오는 데이터가 아니라, 우선순위가 높은 데이터가 먼저 나가는 형태의 자료구조이다.

우선순위 큐는 일반적으로 힙(Heap)을 이용하여 구현한다.

- 우선순위 큐를 힙이 아니라 배열 또는 연결리스트를 이용하여 구현할 수도 있다.
- 하지만 배열과 연결리스트는 선형 구조의 자료구조이므로 삽입 또는 삭제 연산을 위한 시간복잡도는 `O(n)`이다.
    - 최단경로를 찾는 경우 배열이나 리스트는 일반적으로 모든 노드를 순차적으로 탐색하며 최단 경로를 업데이트하기때문에 우선순위큐가 빠름
- 반면 힙트리는 완전이진트리 구조이므로 힙트리의 높이는 `log₂(n+1)`이며, 힙의 시간복잡도는 `O(log₂n)`이다.

![data-structure-heap-priorityqueue](https://github.com/Minsu17/CS-Study/assets/89891511/bdf314d0-8e22-4337-bdf8-1ee243bfc424)


## 우선순위 큐 구현

```java
import java.util.PriorityQueue;

public class PriorityQueueExample {
    public static void main(String[] args) {
        // 우선순위 큐 생성
        PriorityQueue<Integer> pq = new PriorityQueue<>();

        // 요소 추가
        pq.add(10);
        pq.add(30);
        pq.add(20);
        pq.add(5);

        // 요소 삭제 및 출력 (최소값부터 출력됨)
        while (!pq.isEmpty()) {
            System.out.println(pq.poll()); // poll()은 삭제하면서 반환
        }
    }
}
```

### 참고

https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html

https://suyeon96.tistory.com/31
