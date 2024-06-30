# **🔎 트리(Tree) 란?**

트리는 노드와 간선으로 이루어진 계층적 관계를 표현하는 자료구조로 스택이나 큐와 같은 선형 구조가 아닌 비선형 자료구조이다.

트리는 다음과 같은 특징들이 있다.

1. 트리는 하나의 루트 노드를 갖는다.

2. 루트 노드는 0개 이상의 자식 노드를 갖는다.

3. 자식 노드 또한 0개 이상의 자식 노드를 갖는다.

4. 트리는 노드(Node)들과 노드들을 연결하는 간선(Edge)들로 구성되어 있다.

5. N개의 노드를 갖는 트리는 항상 N - 1개의 간선을 갖는다.

6. 모든 자식 노드는 한 개의 부모 노드만을 갖는다.

7. 모든 노드는 서로 연결되어 있다.

8. 임의의 노드에서 다른 노드로 가는 경로(path)는 단 1개만 존재한다

추가로, 트리에는 사이클(Cycle)이 존재할 수 없다. 사이클이란 시작 노드에서 출발해 다른 노드를 거쳐 다시 시작 노드로 돌아올 수 있는 것을 뜻한다. 따라서, 트리는 사이클이 없는 하나의 연결 그래프(Connected Graph)라고 할 수 있다. 당연하게 트리의 노드는 self-loop이 있어서는 안 된다. 즉, 노드 자기 자신과 연결된 간선이 존재해서는 안 된다.

![다운로드](https://github.com/99MinSu/CS-Study/assets/89891084/29c2f1ee-68f8-4272-9bb4-4307f5df9ec3)

이제부터 트리 유사한 그림들을 보면서 트리가 맞는지 아닌지를 살펴보겠다. 

![다운로드 (1)](https://github.com/99MinSu/CS-Study/assets/89891084/3a63ce95-b806-469f-8fe0-1e2c729f1938)

위 그림은 트리가 아니다. 사이클이 있기 때문이다. D에서 시작해 B, C, E를 거치면 다시 D로 올 수 있기 때문에 트리가 아니다.

![다운로드 (2)](https://github.com/99MinSu/CS-Study/assets/89891084/48ffd956-c3fc-4bb6-9617-91649df9e2bb)

위 그림림도 트리가 아니다. 사이클은 없지만 1에서 4로 가는 경로가 유일하지 않기 때문이다. 즉, 1 → 2 → 4로도 4로 가고 1 → 3 → 4를 통해서도 4로 갈 수 있기 때문에 트리가 아니다.

![다운로드 (4)](https://github.com/99MinSu/CS-Study/assets/89891084/e8947802-adf9-4881-b437-59afde1d78e0)

위 그림도 트리가 아니다. 모든 노드들이 연결되어 있는 상태가 아니기 때문에 트리가 아니다.

![다운로드 (3)](https://github.com/99MinSu/CS-Study/assets/89891084/7e395c57-38de-4473-bb8b-bfe5c0a624e6)

# **트리 관련 용어**

트리의 구조    
**루트 노드(root node)** : 부모가 없는 노드로 트리는 단 하나의 루트 노드를 가진다. 부모 노드라고도 불린다. (ex : A)

**단말 노드(leaf node)** : 자식이 없는 노드로 terminal 노드라고도 부른다. (ex : C, D, E)

**내부 노드(internal node)** : 단말 노드가 아닌 노드. 즉, 자식이 있는 노드 (ex : A, B)

**간선(edge)** : 노드를 연결하는 선

**형제(sibling)** : 같은 부모 노드를 갖는 노드들 (ex : D-E, B-C)

**노드의 깊이(depth)** : 루트 노드에서 어떤 노드에 도달하기 위해 거쳐야 하는 간선의 수(ex : D의 depth : 2)

**노드의 레벨(level)** : 트리의 특정 깊이를 가지는 노드의 집합 ( ex : level 1- {B, C} )

**노드의 차수(degree)** : 자식 노드의 개수 (ex : B의 degree - 2, C의 degree - 0)

**트리의 차수(degree of tree)** : 트리의 최대 차수 (ex : 위 트리의 차수는 2이다)

**경로(path)** : 간선으로 연결된, 즉 인접한 노드들로 이뤄진 시퀀스(sequence)를 뜻한다.

**경로 길이(path length)** : 경로에 속한 간선의 수 (ex : A → B → D의 경로 길이는 2가 된다)
 
# **1-1. 트리의 종류**

**Node** 클래스를 아주 간단하게 정의하면 다음과 같습니다.

```java
class Node{
  public String name;
  public Node[] children;
}
```

위의 **Node** 클래스를 포함하는 **Tree**클래스를 정의할 수도 있을 것 입니다.


# **이진 트리(Binary Tree)**

이진 트리는 각 노드가 최대 두 개의 자식을 갖는 트리를 말합니다. 모든 트리가 이진 트리는 아닙니다.
 
<img src="https://github.com/99MinSu/CS-Study/assets/89891084/a3046eeb-c329-4ad6-935f-dd0c92c41b62" width="500" height="300"/>    

위의 그림에서 최대 노드가 3개 이므로 이진 트리라고 할 수 없고 삼진 트리라고 합니다.

# **이진 탐색 트리(Binary Search Tree)**

이진 탐색 트리는 모든 노드가 다음과 같은 특정 순서를 따르는 속성이 있는 이진 트리를 일컫습니다.

`모든 왼쪽 자식들 <= n < 모든 오른쪽 자식들`

이는 모든 노드 n에 대해서 반드시 참이어야 합니다. 부등식의 경우 바로 아래 자식 뿐만 아니라 모든 자식 노드들에 대해서 참이어야 합니다.
   
<img src="https://github.com/99MinSu/CS-Study/assets/89891084/f161e851-be4c-49e2-96a3-407ec0b6f7ee" width="500" height="300"/>

오른쪽 트리의 경우 12가 8의 왼쪽에 있기 때문에 이진 탐색 트리일 수 없습니다.

# **완전 이진 트리(complete binary tree)**

완전 이진 트리는 트리의 모든 높이에서 노드가 꽉 차 있는 이진 트리를 말합니다. 마지막 단계(level)는 꽉 차 있지 않아도 되지만 노드가 왼쪽에서 오른쪽으로 채워져야 합니다.

<img src="https://github.com/99MinSu/CS-Study/assets/89891084/f9161358-24f6-4d44-925b-88065a903cc4" width="500" height="300"/>

# **전 이진 트리(full binary tree)**

전 이진 트리는 모든 노드의 자식이 없거나 정확히 두 개 있는 경우를 말합니다. 즉 자식이 하나만 있는 노드가 존재해서는 안됩니다.

<img src="https://github.com/99MinSu/CS-Study/assets/89891084/191f28d3-5d25-4309-b11f-daabe2326538" width="500" height="300"/>

# **포화 이진 트리(perfect binary tree)**

포화 이진 트리는 전 이진 트리이면서 완전 이진 트리인 경우를 말합니다. 모든 말단 노드는 같은 높이에 있어야 하며, 마지막 단계에서 노드의 개수가 최대가 되어야 합니다. 이진 트리와 포화 이진 트리를 착각 하면 안됩니다.

<img src="https://github.com/99MinSu/CS-Study/assets/89891084/84334729-5d49-44a3-a531-ce9134cbe614" width="300" height="300"/>


# **1-2. 이진 트리 순회**

순회에는 3가지가 있으며 **중위(in-order), 후위(post-order), 전위(pre-order)** 가 있습니다. 그 중 가장 빈번하게 사용되는 것은 중위 순회 입니다.

> 아래의 예제에서 숫자가 나타내는 것은 출력 순서 입니다.
> 

**예제 트리**

<img src="https://github.com/99MinSu/CS-Study/assets/89891084/4d9e9b3c-2263-4c15-96db-4d1b51804ab7" width="300" height="300"/>    

**예제 클래스**

```java
public class Node {
    String value;
    Node left;
    Node right;

    Node(String value){
        this.value = value;
        right = null;
        left = null;
    }
}

public class Main{   
   public static void main(String[] args) {
        Node tree = new Node("A");
        tree.left = new Node("B");
        tree.right = new Node("C");
        tree.left.left = new Node("D");
        tree.left.right = new Node("E");
        tree.right.left = new Node("F");
        tree.right.right = new Node("G");
   }
}
```

# **중위 순회(in-order traversal)**

중위 순회는 왼쪽 가지(branch), 현재 노드, 오른쪽 가지 순서로 노드를 **방문** 하고 출력 합니다.   

<img src="https://github.com/99MinSu/CS-Study/assets/89891084/03b025e9-8bf6-4b73-adf1-f8e6383dfad1" width="300" height="300"/>    

```java
*// 결과 D B E A F C G*
public static void inOrderTraversal(Node node){
    if(node != null){
        inOrderTraversal(node.left);
        System.out.print(node.value);
        inOrderTraversal(node.right);
    }
}
```

# **전위 순회(pre-order traversal)**

전위 순회는 자식 노드보다 현재 노드를 먼저 방문하는 방법 입니다.

<img src="https://github.com/99MinSu/CS-Study/assets/89891084/5eb091ae-d231-46b3-8adc-d76911abcbb0" width="300" height="300"/>    

```java
*// 결과 A B D E C F G*
public static void preOrderTraversal(Node node){
    if(node != null){
        System.out.print(node.value);
        preOrderTraversal(node.left);
        preOrderTraversal(node.right);
    }
}
```

# **후위 순회(post-order traversal)**

후위 순회는 모든 자식 노드를 먼저 방문한 뒤 마지막에 노드를 방문하는 방법 입니다.

<img src="https://github.com/99MinSu/CS-Study/assets/89891084/263534ea-7049-4a81-b18b-b190294ec06f" width="300" height="300"/>    

```java
*// 결과 D E B F G C A*
public static void postOrderTraversal(Node node){
    if(node != null){
        postOrderTraversal(node.left);
        postOrderTraversal(node.right);
        System.out.print(node.value);
    }
}
```
