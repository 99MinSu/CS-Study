# **🔎 그래프(Graph) 란?**

그래프는 **정점 와** **간선**로 이루어진 자료구조이다.

이는 트리(Tree)와 같지만, **트리는 Acyclic**(사이클 x)인 반면 **그래프는 사이클**이 존재한다. (**Cyclic**)

각 **정점(Vertex)** 들이 **간선(Edge)** 들로 연결되어, 연결된 정점 간의 관계를 표현할 수 있는 자료구조이다

![Untitled](https://github.com/99MinSu/CS-Study/assets/89891084/a57854b0-b577-467b-af73-4dd27798e00f)

### 그래프의 구조

- 정점(Vertex) : 노드
- 간선(Edge) : 각 노드간의 연결 선 ( = link, branch)
- 인접 정점(Adjacent Vertex) : 간선 하나만을 통해 바로 연결되어 있는 정점 (정점 1과 정점 4는 인접정점 x)

### **무방향 그래프**

- 정점의 차수(Degree) : 하나의 정점에 인접한 정점의 수 (정점 1의 차수는 2 ), (정점 A의 차수는 3)
    - 무방향 그래프에서 모든 정점 차수의 합은 **그래프 전체 간선 수의 2배**이다.

### **방향 그래프**

- 진입 차수(In-Degree) : 방향 그래프에서 각 정점으로 외부에서 들어오는 간선의 수 (정점 B의 진입 차수는 2)
- 진출 차수(Out-Degree) : 방향 그래프에서 각 정점에서 외부로 나가는 간선의 수 (정점 A의 진출 차수는 3)

### **경로**

- 경로 길이(Path length) : 경로를 구성하는데 사용된 간선의 수
    - 방향그래프에서 **A**에서 **E**로 가는 경우는 여러가지이고, 각각의 경로길이는 다르다.
    - **A** -> B -> D -> **E** : 경로길이=3
    - **A** -> D -> **E** : 경로길이=2
- 단순 경로(Simple path) : 경로 중에서 반복되는 정점이 없는 경우
- 사이클(Cycle) : 단순경로로 한 바퀴 돌아서 다시 같은 노드로 돌아오는 경우
    - 만약 방향그래프 이미지에서 A - D간의 간선이 D에서 A를 향하고 있다면, **A** -> B -> D -> **A**를 사이클이라고 한다.

# **인접 리스트(adjacency list)**

인접 리스트는 그래프를 표현할 때 사용되는 가장 일반적인 방법 입니다. 모든 정점(혹은 노드)을 인접 리시트에 저장 합니다. 무방향 그래프에서 (a, b) 간선은 두 번 저장됩니다. 한 번은 a 정점에서 인접한 간선을 저장하고, 다른 한 번은 b에 인접한 간선을 저장합니다.

그래프에서 노드를 정의하는 간단한 클래스는 트리의 노드 클래스와 궁극적으로 같아 보입니다. 트리에서는 루트 노드에서 모든 노드로 접근이 가능해서 따로 클래스를 두지 않았지만 그래프에서는 가능하지 않아 **Graph** 클래스를 사용합니다.

```java
class Graph{
    public Node[] nodes;
}

class Node{
    public String name;
    public Node[] children;
}
```

위의 그래프는 다음과 같이 표현됩니다.

> 0 : 1
1 : 2
2 : 0, 3
3 : 2
4 : 6
5 : 4
6 : 5
> 

# **인접 행렬**

인접 행렬은 **NxN** boolean Matrix 로써 **matrix[i][j]**가 true라면 연결되어 있다는 뜻 입니다.

<img src="https://github.com/99MinSu/CS-Study/assets/89891084/55e99350-8930-40f1-9a1a-aadf908c6250" width="300" height="300"/>

위와 같은 그래프는 인접 행렬에서 다음과 같이 표현 될 수 있습니다.

|  | 0 | 1 | 2 | 3 |
| --- | --- | --- | --- | --- |
| 0 | 0 | 1 | 0 | 0 |
| 1 | 0 | 0 | 1 | 0 |
| 2 | 1 | 0 | 0 | 0 |
| 3 | 0 | 0 | 1 | 0 |

### 인접 행렬과 인접 리스트 중 선택 방법

### **인접 행렬**

- 그래프 내에 적은 숫자의 간선만을 가지는 희소 그래프(Sparse Graph)의 경우

즉, **노드의 개수가 적고** **간선의 수가 많을 때** 더 낫다.

### **인접 리스트**

- 그래프에 간선이 많이 존재하는 밀집 그래프(Dense Graph)의 경우

즉, **노드의 개수가 많고** **간선의 수가 적을 때** 더 낫다

# **그래프 탐색**

그래프를 탐색하는 일반적인 방법 두 가지로는 **깊이 우선 탐색(depth-first search)**과 **너비 우선 탐색(breadth-first search)**가 있습니다.

- **DFS(깊이 우선 탐색)** : 루트 노드에서 시작해 다음 분기(branch)로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방법 입니다.
- **BFS(너비 우선 탐색)** : 루트 노드에서 시작해서 인접한 노드를 먼저 탐색하는 방법 입니다. 인접한 노드가 여러 개일 때는 노드의 번호 순서대로 순회한다고 가정 합니다.

DFS와 BFS는 서로 다른 상황에서 사용되는 경향이 있습니다. DFS는 그래프에서 모든 노드를 방문하고자 할 때 좀 더 선호되는 편이며, 둘 중 아무거나 사용해도 상관 없지만 깊이 우선 탐색이 좀 더 간단하기는 합니다.

아래의 그래프를 토대로 한번 확인해 보겠습니다.

<img src="https://github.com/99MinSu/CS-Study/assets/89891084/b5ff880f-2fe9-4c52-b0c9-ced4f9da97d8" width="300" height="300"/>    

```java
// 인접 리스트 활용 
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.List;
import java.util.Queue;
public class bfsdfs_list {
    // 정점 0, 1, 2, 3, 4 , 5
    // 연결 정보
    // 0 -> 1, 4, 5
    // 1 -> 4
    // 2 -> 1
    // 3 -> 2, 4
    // 4 
    // 5 
    static List<List<Integer>> adjList = new ArrayList<>();
    static boolean[] visit; // 중복 방문 방지
    public static void main(String[] args) {
        // 자료구조
    	for (int i = 0; i < 6; i++) { // 0 dummy list
			adjList.add(new ArrayList<Integer>()); // 0, 1, 2, 3, 4 ArrayList 객체가 만들어 진다.
		}

        adjList.get(0).add(1);
        adjList.get(0).add(4);
        adjList.get(0).add(5);
        adjList.get(1).add(3);
        adjList.get(1).add(4);
        adjList.get(2).add(1);
        adjList.get(3).add(2);
        adjList.get(3).add(4);
        
        visit = new boolean[6];
    }
}
```

# **깊이 우선 탐색(DFS)**

DFS는 a 노드를 방문한 뒤 a와 인접한 노드들을 차례로 순회 합니다. a와 이웃한 노드 b를 방문했다면, a와 인접한 또 다른 노드를 방문하기 전에 b의 이웃 노드들을 전부 방문해야 합니다. 즉, b의 분기를 전부 완벽하게 탐색한 뒤에야 a의 다른 이웃 노드를 방문할 수 있다는 뜻 입니다.

```java
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.List;
import java.util.Queue;
public class bfsdfs_list {
    // 정점 0, 1, 2, 3, 4 , 5
    // 연결 정보
    // 0 -> 1, 4, 5
    // 1 -> 4
    // 2 -> 1
    // 3 -> 2, 4
    // 4 
    // 5 
    static List<List<Integer>> adjList = new ArrayList<>();
    static boolean[] visit; // 중복 방문 방지
    public static void main(String[] args) {
        // 자료구조
    	for (int i = 0; i < 6; i++) { // 0 dummy list
			adjList.add(new ArrayList<Integer>()); // 0, 1, 2, 3, 4 ArrayList 객체가 만들어 진다.
		}

        adjList.get(0).add(1);
        adjList.get(0).add(4);
        adjList.get(0).add(5);
        adjList.get(1).add(3);
        adjList.get(1).add(4);
        adjList.get(2).add(1);
        adjList.get(3).add(2);
        adjList.get(3).add(4);
        
        visit = new boolean[6];
        
   
				dfs(0);
    }    
    // stack 대신 동일한 효과 더 편한 재귀 호출을 이용
    static void dfs(int n) { // n : 시작 정점
        visit[n] = true;
        
        // 필요한 처리 수행
        System.out.print(n + " -> ");
        
        // 계속 방문을 이어 간다.
        List<Integer> list = adjList.get(n);
        for (Integer i : list) {
						if( visit[i] ) continue;
            dfs(i);
		    }         
    }
}
```

```java
결과
0 1 3 2 4 5
```

# **너비 우선 탐색(BFS)**

BFS도 재귀적으로 동작할 것이라 생각하여 애를 먹는 경우가 많습니다. 그러나 BFS는 재귀적으로 동작하지 않고 큐(queue)를 사용하여 동작하게 됩니다. a 노드에서 시작한다고 했을 때, BFS는 a 노드의 이웃 노드를 모두 방문한 다음 이웃의 이웃들을 방문 합니다.

```java
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.List;
import java.util.Queue;
public class bfsdfs_list {
    // 정점 0, 1, 2, 3, 4 , 5
    // 연결 정보
    // 0 -> 1, 4, 5
    // 1 -> 4
    // 2 -> 1
    // 3 -> 2, 4
    // 4 
    // 5 
    static List<List<Integer>> adjList = new ArrayList<>();
    static boolean[] visit; // 중복 방문 방지
    public static void main(String[] args) {
        // 자료구조
    	for (int i = 0; i < 6; i++) { // 0 dummy list
			adjList.add(new ArrayList<Integer>()); // 0, 1, 2, 3, 4 ArrayList 객체가 만들어 진다.
		}

        adjList.get(0).add(1);
        adjList.get(0).add(4);
        adjList.get(0).add(5);
        adjList.get(1).add(3);
        adjList.get(1).add(4);
        adjList.get(2).add(1);
        adjList.get(3).add(2);
        adjList.get(3).add(4);
        
        visit = new boolean[6];
        
        bfs(0);
    }
    static void bfs(int n) { // n : 시작 정점
        Queue<Integer> queue = new ArrayDeque<>();
        queue.offer(n);
        visit[n] = true;
        
        while(! queue.isEmpty() ) {
            // 정점을 꺼낸다.
            int v = queue.poll();
            
            // 필요한 처리 수행
            System.out.print(v + " -> ");
            
            // 계속 방문을 이어 간다.
            List<Integer> list = adjList.get(v);
            for (Integer i : list) {
                if( visit[i] ) continue;
                queue.offer(i);
                visit[i] = true;
            }                     
        }
    }
}

```

```java
결과
0 1 4 5 3 2
```
