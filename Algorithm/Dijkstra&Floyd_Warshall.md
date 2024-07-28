# 최단경로 알고리즘(Dijkstra & Floyd Warshall)

# 다익스트라(Dijkstra)

## 개요

다익스트라(dijkstra) 알고리즘은 **음의 가중치**(음의 간선, 음의 값)**가 없는 그래프의 한 노드**에서 **각 모든 노드까지의 최단거리를 구하는 알고리즘**을 말한다.

이 과정에서 도착 정점 뿐만 아니라 모든 다른 정점까지 최단 경로로 방문하며 각 정점까지의 최단 경로를 모두 찾게 된다. 매번 최단 경로의 정점을 선택해 탐색을 반복하는 것이다.

참고로 그래프 알고리즘 중 최소 비용을 구하는 데는 다익스트라 알고리즘 외에도 벨만-포드 알고리즘, 프로이드 워샬 알고리즘 등이 있다.

다익스트라 알고리즘은 **그리디 알고리즘**이자 **다이나믹 프로그래밍 기법을 사용한 알고리즘**이라고 볼 수 있다.

## 메커니즘

다익스트라 알고리즘의 메커니즘은 기본적으로

아래 두 단계를 반복하여 임의의 노드에서 각 모든 노드까지의 최단거리를 구하는 문제에서 활용할 수 있다.

임의의 노드에서 다른 노드로 가는 값을 비용이라고 한다.

- **방문하지 않은 노드** **중**에서 **가장 비용이 적은 노드를 선택**한다(그리디 알고리즘)
- **해당 노드로부터 갈 수 있는 노드들의 비용을 갱신**한다(다이나믹 프로그래밍)

가능한 적은 비용으로 가장 빠르게 해답에 도달하는 경로를 찾아내는 대부분의 문제에 응용되며, 적용하는 문제를 그림으로 살펴보며 이해해 보자.

## 다익스트라 동작 단계

**A노드에서 출발하여 F노드로 가는 최단 경로를 구하는 문제**를 다익스트라 알고리즘을 활용한다.

아래의 각 데이터의 의미를 보며 살펴보자

- S = 방문한 노드들의 집합
- d [N] = A → N까지 계산된 최단 거리
- Q = 방문하지 않은 노드들의 집합
- 확인되지 않은 거리는 전부 초기값을 무한으로 잡는다 ex) INF

![image](https://github.com/user-attachments/assets/a6dc79a1-529a-44b7-8808-a54ba51e0a6e)


- 출발지와 출발지의 거리는 확인해 볼 필요도 없이 당연히 0 값을 가진다는 것을 알 수 있다. 출발지를 A로 설정했기 때문에, d[A]=0이 된다. (A노드를 아직 방문한 것은 아니다.)
- 출발지를 제외한 모든 노드들도 아직 확인되지 않았기에, d[다른 노드]=무한이 된다.
- Q는 방문하지 않은 노드들의 집합이므로, 초기화할 때는 모든 노드들의 집합이 된다.
- S는 방문한 노드가 아직 없으므로 공집합 상태이다.

1. **루프를 돌려 이웃 노드를 방문하고 거리를 계산한다.**

![image](https://github.com/user-attachments/assets/48086c7c-cde4-47dc-b051-17c8a048e3e8)


**2. 첫 루프 이후의 그래프의 상태가 업데이트되는 방식**

![image](https://github.com/user-attachments/assets/25c9ab7a-9ab8-4141-b92f-5ed6222342d5)


**3. 더 빠른 경로를 발견한 경우 ( d[C] = 5->4 ) 값 업데이트**

![image](https://github.com/user-attachments/assets/ab39971f-0685-47bc-b498-49cf608bbe50)


이런 식으로 방문하지 않은 노드 중 비용이 적은 노드를 선택하여 가까운 노드의 비용**(그리드 알고리즘)과**

해당 노드로부터 갈 수 있는 노드들의 비용을 갱신한다. **(다이나믹 프로그래밍)을** 반복하여 사용한다.

**3.1 더 빠른 경로를 발견한 경우 ( d[E] = 10->6 , d[F] = 11->9) 값 업데이트**

![image](https://github.com/user-attachments/assets/53350182-c2ac-4318-a77c-fcfa25636101)


E노드에 왔을 때 d[F] = 9 -> 8 값 업데이트

![image](https://github.com/user-attachments/assets/00a236fd-272b-4740-a6f4-540da6bbc629)


이 일련의 과정이 반복되어 Q가 공집합이 되었다면, 남아 있는 데이터로 추론하여 최단 거리를 결정한다.

마지막 루프 이후,

![image](https://github.com/user-attachments/assets/05756778-2541-432e-868c-c8197f343036)


S = {A, B, D, C, E, F} (방문한 순서대로 정렬)

- d[A] = 0
- d[B] = 2
- d[C] = 4
- d[D] = 3
- d[E] = 6
- d[F] = 8
- Q = ∅

목적지가 F였으므로, A→D→C→E->F가 최단 경로이며, 거리는 8로 결정된다

## 구현

인접리스트 사용

```java
import java.util.*;

public class DijkstraExample {

    public static void dijkstra(List<List<int[]>> graph, int source) {
        int V = graph.size();
        int[] dist = new int[V];
        Arrays.fill(dist, Integer.MAX_VALUE); // 모든 거리를 무한대로 초기화
        dist[source] = 0; // 시작점의 거리는 0

        // 우선순위 큐를 사용하여 거리 기준으로 정렬
        PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(pair -> pair[1]));
        pq.add(new int[]{source, 0});

        while (!pq.isEmpty()) {
            int[] current = pq.poll(); // 가장 가까운 정점을 꺼냄
            int u = current[0];

            for (int[] neighbor : graph.get(u)) { // 현재 정점과 연결된 모든 인접 정점을 확인
                int v = neighbor[0];
                int weight = neighbor[1];

                if (dist[u] + weight < dist[v]) { // 더 짧은 경로를 발견하면 거리 갱신
                    dist[v] = dist[u] + weight;
                    pq.add(new int[]{v, dist[v]}); // 갱신된 거리로 큐에 추가
                }
            }
        }

        // 결과 출력
        System.out.println("정점 \t 거리");
        for (int i = 0; i < V; i++) {
            System.out.println(i + " \t\t " + dist[i]);
        }
    }

    public static void main(String[] args) {
        int V = 5;
        List<List<int[]>> graph = new ArrayList<>();
        for (int i = 0; i < V; i++) {
            graph.add(new ArrayList<>()); // 각 정점의 인접 리스트 초기화
        }

        // 간선 추가: {목적지, 가중치}
        graph.get(0).add(new int[]{1, 9}); -> 0과 1이 인접, 가중치 9
        graph.get(0).add(new int[]{2, 6}); -> 0과 2이 인접, 가중치 6
        graph.get(0).add(new int[]{3, 5});
        graph.get(0).add(new int[]{4, 3});
        graph.get(2).add(new int[]{1, 2});
        graph.get(2).add(new int[]{3, 4});

        // 다익스트라 알고리즘 실행
        dijkstra(graph, 0);
    }
}

```

## 특징

**장점**

- 인접 행렬 또는 우선순위 대기열을 사용하여 구현할 수 있으므로 가능한 모든 경로를 확인하는 무차별 접근 방식보다 효율적이다.
- 거리뿐만 아니라 경로를 추적하도록 알고리즘을 쉽게 수정할 수 있다.

**단점**

- 우선순위 대기열을 사용할 때 간선이 많은 큰 그래프의 경우 느려질 수 있다.
- 그래프와 거리를 저장하려면 많은 양의 메모리가 필요하다.
- 동일한 거리에 여러 경로가 있는 경우 최상의 경로를 보장하지 않는다.
- 지형이나 교통 상황과 같은 다른 요소는 고려하지 않는다.

# 플로이드 워셜(Floyd Warshall)

## 개요

- **'모든 지점에서 다른 모든 지점까지의 최단 경로를 모두 구해야 하는 경우'**에 사용할 수 있는 알고리즘
- 소스코드가 다익스트라에 비해 매우 짧아 구현이 쉽다.
- 다익스트라의 경우 단계마다 최단 거리를 가지는 노드를 하나씩 반복적으로 선택한다. 이후 해당 노드를 거쳐가는 경로를 확인하며 최단 거리 테이블을 갱신하는 방식으로 동작한다.
    
    **<-->** **플로이드 워셜 알고리즘** 또한 단계마다 '거쳐 가는 노드'를 기준으로 알고리즘을 수행한다. 하지만, 매 단계마다 방문하지 않은 노드 중에서 최단 거리를 갖는 노드를 찾을 필요가 없다!
    
- 플로이드 워셜은 2차원 테이블에 최단 거리 정보를 저장한다. (모든 지점에서 다른 모든 지점까지의 최단 거리를 저장해야 하기 때문이다.)
    
    **<-->** 다익스트라는 한 지점에서 다른 지점까지의 최단 거리이기 때문에 1차원 리스트에 저장한다.
    
- 플로이드 워셜 알고리즘은 DP 알고리즘에 속한다. 왜냐하면 만약 노드의 개수가 `N`개라고 할 때, `N`번 만큼의 단계를 반복하며 '점화식에 맞게' 2차원 리스트를 갱신하기 때문에 DP라고 볼 수 있다.
    
    **<-->** 다익스트라는 그리디 알고리즘에 속한다고 볼 수 있다.
    

![image](https://github.com/user-attachments/assets/4850254f-629b-4457-8623-e69f1245cdb6)


## 플로이드 워셜 동작 단계

**[step 0]** 그래프의 노드와 간선에 따라 최단 거리 테이블을 갱신한다.

![image](https://github.com/user-attachments/assets/454ce2e9-5d02-4133-853d-12bb8d77b473)


**[step 1]** 1번 노드를 거쳐 가는 경우를 고려하여 테이블을 갱신한다.

![image](https://github.com/user-attachments/assets/f34bf72a-56e7-4523-bb0f-9ab1242a9edc)


**[step 2]** 2번 노드를 거쳐 가는 경우를 고려하여 테이블을 갱신한다.

![image](https://github.com/user-attachments/assets/1bc0b841-94de-420b-bbae-1e741e896744)


**[step ~]** 3번, 4번, ... 노드를 거쳐 가는 경우를 고려하여 테이블을 갱신한다.

![image](https://github.com/user-attachments/assets/97665f67-65d6-448b-920a-b38d0f120e64)


![image](https://github.com/user-attachments/assets/2ee4280d-eea4-4d23-8811-d46762fd0c38)


## 구현

```java
public class FloydWarshall {

    final static int INF = 99999; // 무한대를 나타내기 위한 큰 값

    public static void floydWarshall(int[][] graph) {
        int V = graph.length;
        int[][] dist = new int[V][V];

        // 거리 배열 초기화
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                dist[i][j] = graph[i][j];
            }
        }

        // 플로이드-워셜 알고리즘
        for (int k = 0; k < V; k++) {
            for (int i = 0; i < V; i++) {
                for (int j = 0; j < V; j++) {
                    if (dist[i][k] != INF && dist[k][j] != INF && dist[i][k] + dist[k][j] < dist[i][j]) {
                        dist[i][j] = dist[i][k] + dist[k][j];
                    }
                }
            }
        }

        // 결과 출력
        printSolution(dist);
    }

    public static void printSolution(int[][] dist) {
        int V = dist.length;
        System.out.println("정점 쌍 사이의 최단 거리 행렬:");
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                if (dist[i][j] == INF) {
                    System.out.print("INF ");
                } else {
                    System.out.print(dist[i][j] + " ");
                }
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        int[][] graph = {
            {0, 5, INF, 10},
            {INF, 0, 3, INF},
            {INF, INF, 0, 1},
            {INF, INF, INF, 0}
        };

        floydWarshall(graph);
    }
}

```

- 이 알고리즘은 인접 행렬을 사용하여 구현하는 것이 적합
- 인접 행렬은 O(1) 시간에 특정 두 정점 사이의 가중치에 접근할 수 있어, 플로이드-워셜 알고리즘의 세 개의 중첩 루프 구조에 최적화
- 인접 리스트는 메모리를 절약할 수 있지만, 플로이드-워셜 알고리즘에서는 그 이점을 살리기 어려움

### Reference

[https://cobi-98.tistory.com/46#�%-B%A-�%-D%B-�%-A%A-�%-A%B-�%-D�%--�%--%-C�%B-%A-�%A-��%A-%--%--�%B-%B-�%A-�%--�%--%A-��%--](https://cobi-98.tistory.com/46#%EB%25-B%25A-%EC%25-D%25B-%EC%25-A%25A-%ED%25-A%25B-%EB%25-D%BC%25--%EC%25--%25-C%EA%25B-%25A-%EB%25A-%AC%EC%25A-%25--%25--%EA%25B-%25B-%EB%25A-%BC%25--%EC%25--%25A-%EB%AA%25--)

[https://velog.io/@717lumos/알고리즘-다익스트라Dijkstra-알고리즘](https://velog.io/@717lumos/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%8B%A4%EC%9D%B5%EC%8A%A4%ED%8A%B8%EB%9D%BCDijkstra-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)

[https://velog.io/@kimdukbae/플로이드-워셜-알고리즘-Floyd-Warshall-Algorithm](https://velog.io/@kimdukbae/%ED%94%8C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%9B%8C%EC%85%9C-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-Floyd-Warshall-Algorithm)
