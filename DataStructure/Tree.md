# **🔎 트리(Tree) 란?**

# **1-1. 트리의 종류**

트리는 노드(Node)로 이루어진 자료구조 입니다. 트리를 이해하기 위한 좋은 방법 중 하나는 재귀적 설명법을 사용하는 것 입니다.

- 트리는 하나의 루트 노드를 갖는다.(그래프 이론에서 꼭 이래야할 필요는 없지만, 보통 일반적인 프로그래밍, 면접의 트리에선 맞는 말이라고 할 수 있습니다.)
- 루트 노드는 0개 이상의 자식 노드를 갖고 있다.
- 그 자식 노드 또한 0개 이상의 자식 노드를 갖고 있고, 이는 반복적으로 정의 된다.

트리에는 사이클(cycle)이 존재할 수 없습니다. 노드들은 특정 순서로 나열될 수도 있고 없을 수도 있습니다. 각 노드는 부모 노드로의 연결이 있을 수도 있고 없을 수도 있습니다.

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
