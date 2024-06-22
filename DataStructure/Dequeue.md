### Dequeue(덱)

Dequeue란 "Double-ended Queue”의 약자로 양쪽 끝에서 삽입과 삭제가 모두 가능한 자료구조이다.

![다운로드 (4).png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/8a03dd86-558a-4c30-b4ba-bdf9140cb219/%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C_(4).png)

- 양방향에서 삽입, 삭제 연산이 가능한 큐를 말한다.
- 따라서 Stack과 Queue를 모두 구현할 수 있다.
- 선입선출(FIFO)과 후입선출(LIFO) 개념이 모두 적용될 수 있다.

**Dequeue 용어**

- 스크롤(Scroll) : 한 방향으로만 입력이 가능한 덱(입력 제한 덱, 출력은 양쪽에서 일어날 수 있다.)
- 셸프(Shelf) : 한 방향으로만 출력이 가능한 덱(출력 제한 덱, 입력은 양쪽에서 일어날 수 있다.)

![다운로드 (3).png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/9ee36b06-50a0-48a9-9fc5-544e9c3b8843/0885d673-095c-4a9d-bae4-21ab3a089887.png)

**Dequeue의 구현**

Java에서 덱은 java.util.Deque 인터페이스를 구현한  `ArrayDeque`와 `LinkedList` 클래스를 사용하여 구현할 수 있다.

- ArrayDeque : `ArrayDeque`는 내부적으로 동적 배열을 사용하여 구현

```java
ArrayDeque<Integer> deque = new ArrayDeque<>();
```

- LinkedList : `LinkedList`는 이중 연결 리스트로 구현

```java
Deque<String> deque = new LinkedList<>();
```

**Dequeue의 사용법**

- 삽입 관련 메소드

![img1.daumcdn.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/0324216d-15e6-4642-ba8b-a00d3244160b/img1.daumcdn.png)

```java

ArrayDeque<Integer> deque = new ArrayDeque<>();

// addFirst() 메서드: 덱의 앞에 요소를 추가하고, 덱이 가득 차면 예외가 발생한다.
deque.addFirst(1);  // deque: [1], push()

// addLast() 메서드 : 덱의 마지막에 요소를 추가하고, 덱이 가득 차면 예외가 발생한다.
deque.addLast(2);   // deque: [1, 2] , add()

// addLast() 메서드: 덱의 앞에 요소를 추가하고, 정상적으로 수행된 경우 true, 가득찬 경우 false를 리턴한다.
deque.offerFirst(3);  // deque: [3, 1, 2]

// addLast() 메서드: 덱의 마지막에 요소를 추가하고, 정상적으로 수행된 경우 true, 가득찬 경우 false를 리턴한다.
deque.offerLast(4);   // deque: [3, 1, 2, 4]
```

- 삭제 관련 메소드

![img1.daumcdn.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/f79e53f1-2709-4088-94ad-5fbef40b3a0e/img1.daumcdn.png)

```java
// removeFirst() 메서드: 덱의 앞에 요소를 추가하고, 덱이 비어있으면 예외가 발생.
deque.removeFirst();  // element(), pop()

// pollFirst() 메서드: 덱의 앞 요소 제거 및 반환, 덱이 비어있으면 null 리턴.
deque.pollFirst(); //poll()

// removeLast() 메서드: 덱의 마지막 요소 제거 및 반환, 덱이 비어있으면 예외가 발생.
deque.removeLast();  

// pollLast() 메서드: 덱의 마지막에 요소를 추가하고, 덱이 비어있으면 null 리턴.
deque.pollLast();   
```

- 조회 관련 메소드

![img1.daumcdn.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/14c554f1-58ff-480e-9b9e-b3b9654487ed/img1.daumcdn.png)

```java
// getFirst() 메서드: 덱의 앞 요소 반환 (제거하지 않음), 덱이 비어있으면 예외가 발생.
deque.getFirst();  

// peekFirst() 메서드: 덱의 앞 요소 반환 (제거하지 않음), 덱이 비어있으면 null을 반환.
deque.peekFirst();  // peek()

// getLast() 메서드: 덱의 마지막 요소 반환 (제거하지 않음), 덱이 비어있으면 예외가 발생.
deque.getLast();  

// peekLast() 메서드: 덱의 마지막 요소 반환 (제거하지 않음), 덱이 비어있으면 null을 반환.
deque.peekLast();   
```
