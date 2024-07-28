# **DFS(Depth-First Search)와 BFS(Breadth-First Search)**

DFS(Depth-First Search)와 BFS(Breadth-First Search)는 그래프를 탐색하는 두 가지 기본적인 알고리즘이다.

- 그래프 탐색이란 하나의 정적으로부터 시작하여 차례대로 모든 정점들을 한 번씩 방문하는 것을 말한다.
- 두 알고리즘 모두 **그래프의** **모든 노드를 방문하는 것을 목표**로 하지만, 탐색 방식이 다르다
- 그래프? https://github.com/99MinSu/CS-Study/blob/main/DataStructure/Graph.md

## 깊이 우선 탐색 (DFS, **Depth-First Search)**

DFS는 그래프 탐색 알고리즘 중 하나로, 가능한 한 깊게 탐색한 후 더 이상 갈 곳이 없으면 되돌아와서 다른 경로를 탐색하는 방식을 사용하는 알고리즘이다.

- DFS는 그래프의 모든 노드를 방문하고, 각 노드를 한 번씩 방문하여 깊이 우선으로 탐색하는 것을 목표로 한다.
- DFS는 스택이나 재귀 호출을 사용하여 구현한다.
- DFS는 A에서 B로 가는 모든 경로를 찾거나 경로의 특정 특성을 저장하는 데 유리하다.

### 깊이 우선 탐색의 탐색 과정

![깊이 우선 탐색의 탐색 과정](https://github.com/user-attachments/assets/5b6606ab-5f0e-4529-a61a-5a0bb2b7a7d8)

- 시작 노드를 방문하고 방문 처리를 합니다.
- 방문한 노드와 인접한 노드 중에서 방문하지 않은 노드를 찾아 방문합니다.
- 더 이상 방문할 노드가 없을 때까지 이 과정을 반복합니다.
- 더 이상 방문할 노드가 없으면 이전 노드로 돌아가서 다른 경로를 탐색합니다.

---

### 깊이 우선 탐색의 구현

DFS(Depth-First Search, 깊이 우선 탐색)을 구현하는 방법은 재귀를 사용하는 방법과 스택을 사용하는 방법 2가지가 있다.

- 그래프 탐색의 경우 어떤 노드를 방문했었는지 여부를 반드시 검사 해야 한다. )검사하지 않을 경우 무한루프에 빠질 위험이 있다.)

**공통 코드(인접 행렬 사용)**

```java
public class DefaultDFS {
    private static int n; // 정점의 수
    private static int[][] e; // 인접 행렬
    private static boolean[] dfsVisited; // DFS 방문 여부를 저장하는 배열

    public static void main(String[] args) {
        n = 5; // 예시 정점의 수
        e = new int[n + 1][n + 1]; // 인접 행렬 초기화
        dfsVisited = new boolean[n + 1];
        
        // 인접 행렬 예시 초기화
        // e[u][v] = 1은 정점 u와 정점 v 사이에 간선이 있음을 의미합니다.
        // 그래프에 맞게 간선을 추가합니다.
        
        dfs(1); // DFS 시작 정점
    }
}
```

### **재귀적 구현**

재귀적 DFS는 **함수 호출 스택을 사용하여 구현**된다.

- 함수 호출 스택이 암묵적으로 각 노드 방문 상태를 저장하기 때문에 별도의 스택 자료구조를 사용할 필요가 없다. (구현이 간단하고 코드가 직관적이다.)

```java
public void dfs(int vertex) {
    System.out.print(vertex + " "); // 현재 정점 출력
    dfsVisited[vertex] = true; // 현재 정점을 방문한 것으로 표시
    for (int i = 1; i <= n; i++) { // 모든 정점을 순회
        if (e[vertex][i] == 1 && !dfsVisited[i]) { // 인접 정점이고 방문하지 않은 경우
            dfs(i); // 재귀적으로 DFS 수행
        }
    }
}
```

### **명시적 스택을 사용한 구현**

스택을 사용한 DFS는 명시적인 스택 자료구조를 사용하여 구현된다.

- 이 방법은 재귀 호출의 깊이가 제한적일 때 유용하며, 스택을 사용하여 DFS를 명시적으로 제어할 수 있다.

```java
public void dfs(int startVertex) {
    Stack<Integer> stack = new Stack<>();
    stack.push(startVertex);
    dfsVisited[startVertex] = true;

    while (!stack.isEmpty()) {
        int vertex = stack.pop();
        System.out.print(vertex + " "); // 현재 정점 출력

        for (int i = 1; i <= n; i++) { // 모든 정점을 순회
            if (e[vertex][i] == 1 && !dfsVisited[i]) { // 인접 정점이고 방문하지 않은 경우
                stack.push(i); // 정점을 스택에 추가
                dfsVisited[i] = true; // 정점을 방문한 것으로 표시
            }
        }
    }
}
```

---

## **너비 우선 탐색 (BFS, Breadth-First Search)**

**BFS는** 그래프 탐색 알고리즘 중 하나로, 시작 노드에서부터 인접한 노드를 모두 탐색한 후, 인접한 노드들의 인접 노드를 탐색하는 방식을 사용하는 알고리즘이다.

- BFS는 깊이보다는 너비를 우선으로 탐색하여, 시작 노드로부터 가까운 노드를 먼저 탐색한다.
- BFS는 최단 경로를 보장하고 레벨 기반 탐색에 유리하다.

### 너비 우선 탐색의 탐색 과정

![너비 우선 탐색의 탐색 과정](https://github.com/user-attachments/assets/af4ba33e-a75c-4c60-873e-e46397486033)

- 시작 노드를 큐에 넣고 방문 처리를 합니다.
- 큐에서 노드를 하나씩 꺼내고, 그 노드와 인접한 방문하지 않은 노드를 모두 큐에 넣습니다.
- 큐가 빌 때까지 이 과정을 반복합니다.

### 너비 우선 탐색의 구현

```java
public class DefaultBFS {
    private static int n; // 정점의 수
    private static int[][] e; // 인접 행렬
    private static boolean[] bfsVisited; // BFS 방문 여부를 저장하는 배열

    public static void main(String[] args) {
        n = 5; // 예시 정점의 수
        e = new int[n + 1][n + 1]; // 인접 행렬 초기화
        bfsVisited = new boolean[n + 1];
        
        // 인접 행렬 예시 초기화
        // e[u][v] = 1은 정점 u와 정점 v 사이에 간선이 있음을 의미합니다.
        // 그래프에 맞게 간선을 추가합니다.
        
        bfs(1); // BFS 시작 정점
    }

    // 너비 우선 탐색 (BFS)
    public static void bfs(int vertex) {
        Queue<Integer> q = new LinkedList<>(); // 큐 초기화
        q.add(vertex); // 시작 정점을 큐에 추가
        bfsVisited[vertex] = true; // 시작 정점을 방문한 것으로 표시
        while (!q.isEmpty()) { // 큐가 비어 있지 않은 동안 반복
            int tmp = q.poll(); // 큐에서 정점을 꺼냄
            System.out.print(tmp + " "); // 현재 정점 출력
            for (int i = 1; i <= n; i++) { // 모든 정점을 순회
                if (!bfsVisited[i] && e[tmp][i] == 1) { // 인접 정점이고 방문하지 않은 경우
                    q.add(i); // 정점을 큐에 추가
                    bfsVisited[i] = true; // 정점을 방문한 것으로 표시
                }
            }
        }
    }
}
```

---

# 시간 복잡도

그래프(정점의 수: V, 간선의 수: E)의 모든 간선을 조회하는 경우

### **인접 리스트를 이용**

<img width="1195" alt="인접 리스트" src="https://github.com/user-attachments/assets/088a055f-51e0-4ca0-a3aa-eec04640e781">

- 각 점정을 한 번씩 방문, V개의 정점을 방문하는데 $O(V)$의 시간이 소요, 각 정점에 인접한 모든 정점을 확인하여 그래프의 모든 간선 E 을 한번씩 검사한다. 따라서 인점 정점을 탐색하는데 $O(E)$이 소요된다.
- **시간 복잡도**: $O(N+E)$
- **인접 리스트**는 희소 그래프(간선의 수가 정점의 수에 비해 상대적으로 적을 때), 메모리 효율이 중요할 때, 빠른 인접 정점 접근이 필요할 때 적합합니다.

### **인접 행렬를 이용**

<img width="1258" alt="인접 행렬" src="https://github.com/user-attachments/assets/363ef207-4615-4d3e-8b51-3c5f9a534636">

- 각 점정을 한 번씩 방문, V개의 정점을 방문하는데 $O(V)$의 시간이 소요되고, 정점마다 인접한 정점을 찾기 위해 행렬의 해당 행을 탐색 하지만 각 행은 V개의 요소를 가지고 있기 떄문에 $O(V^2)$이 소요된다.
- **시간 복잡도**: $O(V^2)$
- **인접 행렬**은 밀집 그래프(간선의 수가 정점의 수에 비해 상대적으로 많을 때), 간선 존재 여부를 빠르게 확인해야 할 때, 작은 그래프에서 적합합니다.

DFS와 BFS는 시간 복잡도는 같지만, 탐색 방식과 용도에서 차이가 있기 때문에 특성과 문제의 요구사항에 따라 적절한 탐색 방법을 선택해야 한다.

- DFS: 경로 탐색, 순환 탐지, 백트래킹 문제 (예: 미로 찾기, 퍼즐 문제).
- BFS: 최단 경로 찾기 (비가중치 그래프), 레벨 탐색 (예: 최단 거리, 최단 단계).

---

## DFS vs BFS 요약

| 특성 | DFS | BFS |
| --- | --- | --- |
| 탐색 순서 | 깊이 우선 탐색 | 너비 우선 탐색 |
| 최단 경로 보장 | 보장하지 않음 | 무방향 그래프에서 최단 경로 보장 (가중치가 동일한 경우) |
| 메모리 사용 | 깊이에 따라 달라짐 (재귀적 호출 시 스택 사용) | 너비에 따라 달라짐 (큐를 사용하여 현재 레벨의 모든 노드 저장) |
| 경로 탐색 | 모든 경로를 탐색하여 찾기 가능 | 최단 경로를 찾는 데 유용 |
| 구현 | 재귀적 호출 또는 명시적 스택 사용 | 큐를 사용하여 구현 |

**Reference**

https://sarah950716.tistory.com/12

https://devuna.tistory.com/32
