# Dequeue(덱)

Dequeue란 "Double-ended Queue”의 약자로 양쪽 끝에서 삽입과 삭제가 모두 가능한 자료구조이다.
![덱](https://github.com/OkKim99/CS-Study/assets/89891488/d60aaa7b-2ae9-406d-8cb4-f6ce5387d982)


- 양방향에서 삽입, 삭제 연산이 가능한 큐를 말한다.
- 따라서 Stack과 Queue를 모두 구현할 수 있다.
- 선입선출(FIFO)과 후입선출(LIFO) 개념이 모두 적용될 수 있다.

## Dequeue 용어

- 스크롤(Scroll) : 한 방향으로만 입력이 가능한 덱(입력 제한 덱, 출력은 양쪽에서 일어날 수 있다.)
- 셸프(Shelf) : 한 방향으로만 출력이 가능한 덱(출력 제한 덱, 입력은 양쪽에서 일어날 수 있다.)

## Dequeue의 구현

Java에서 덱은 java.util.Deque 인터페이스를 구현한  `ArrayDeque`와 `LinkedList` 클래스를 사용하여 구현할 수 있다.

- ArrayDeque : `ArrayDeque`는 내부적으로 동적 배열을 사용하여 구현

```java
ArrayDeque<Integer> deque = new ArrayDeque<>();
```

- LinkedList : `LinkedList`는 이중 연결 리스트로 구현

```java
Deque<String> deque = new LinkedList<>();
```

## Dequeue의 사용법

- 삽입 관련 메소드
<img width="450" alt="삽입" src="https://github.com/OkKim99/CS-Study/assets/89891488/4dc324eb-3ae9-40c3-94a8-e5505ac052b2">

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
<img width="450" alt="삭제" src="https://github.com/OkKim99/CS-Study/assets/89891488/1ddc9669-f50f-4e2e-b57c-86ebfd5d3483">

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
<img width="450" alt="조회" src="https://github.com/OkKim99/CS-Study/assets/89891488/7bf1427d-fa39-47dc-845b-9ef428e28b55">

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
