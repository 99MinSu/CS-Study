## 1) 백트래킹 (BackTracking)

- **퇴각 검색이라고도 불리며 재귀적으로 문제를 해결**하되 현재 재귀를 통해 확인 중인 상태가 제한 조건에 위배가 되는지 판단하고, 해당 상태가 위배되는 경우 **해당 상태를 제외**하고 다음 단계로 넘어갑니다.
- 말이 어렵지만, 위에서 말한 대로 **해를 찾는 도중 해가 절대 될 수 없다고 판단되면, 되돌아가서 다시 해를 찾는다**고 생각하면 됩니다.
- 주로 DFS와 함께 사용됩니다.
- 여기서 **KEY POINT**는 더 이상 탐색할 필요가 없는 상태를 제외한다는 것인데, 이를 **가지치기**라고 합니다.

## 2) 간단한 예시 중복 없이 수열 구하기 ( N 과 M (1) )

백준 백트래킹 카테고리 첫 번째 문제인 N과 M으로 간단하게 알아봅시다.

https://www.acmicpc.net/problem/15649

![화면 캡처 2024-07-28 124644](https://github.com/user-attachments/assets/aea81749-3e32-43eb-a25f-7d8cf748ede1)

문제를 보면 중복을 제외하고 모든 경우의 수를 탐색해야 되는 걸 알 수 있습니다.

그러면 dfs를 활용하면 되겠다는 생각을 가지고 dfs 함수에는 N과 M을 변수로 받아야하는 걸 생각하고 dep 변수 (깊이) 를 추가해야합니다. dep를 통해 재귀가 깊어질 때마다 dep를 1씩 증가시켜 M과 같아지면 더이상 재귀를 호출하지 않고 탐색과정 중 값을 담았던 arr 배열을 출력해주고 return 하는 역할을 위해서입니다.

```
    arr = new int[m];
	visit = new boolean[n+1]; // 1부 N까지 체크해주기 위해 n+1

    static void dfs(int x, int y, int dep) {

    	// 재귀 깊이가 같아지면 탐색 과정에서 담았던 배열을 StringBuilder 에 추가해준다.
    	if(dep == m) {
			for (int val : arr) {
				sb.append(val).append(' ');
			}
			sb.append('\n');
			return;
    	}

		for (int i = 1; i <= n; i++) { // 1부터 시작
			if (!visit[i]) { // 방문하지 않았으면??
				visit[i] = true; // 방문 상태로 변경
				arr[dep] = i; // 해당 깊이를 인데스로 하여 i 저장
				dfs(x, y, dep + 1); // 다음 방문을 위해 dep + 1 증가시키면서 재귀 호출
				visit[i] = false; // 방문이 끝나고 돌아오면 방문하지 않은 상태로 되돌린다.
			}
		}
    }
```

## 3) N 과 M (1) 전체 코드

```
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
	static int n, m;
	static int[] arr;
	static boolean[] visit;
	static StringBuilder sb = new StringBuilder();
    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

		arr = new int[m];
		visit = new boolean[n+1]; // 1부 N까지 체크해주기 위해 n+1
		dfs(n, m, 0);

		System.out.println(sb);

    }

    static void dfs(int x, int y, int dep) {

    	// 재귀 깊이가 같아지면 탐색 과정에서 담았던 배열을 StringBuilder 에 추가해준다.
    	if(dep == m) {
			for (int val : arr) {
				sb.append(val).append(' ');
			}
			sb.append('\n');
			return;
    	}

		for (int i = 1; i <= n; i++) { // 1부터 시작
			if (!visit[i]) { // 방문하지 않았으면??
				visit[i] = true; // 방문 상태로 변경
				arr[dep] = i; // 해당 깊이를 인데스로 하여 i 저장
				dfs(x, y, dep + 1); // 다음 방문을 위해 dep + 1 증가시키면서 재귀 호출
				visit[i] = false; // 방문이 끝나고 돌아오면 방문하지 않은 상태로 되돌린다.
			}
		}
    }
}
```

중요 key point는 boolean 타입 visit 배열을 통해 방문 한 곳이면 탐색하지 않고 가지 치기를 해주고 모든 노드를 탐색하기 위해 다시 방문하지 않은 상태로 돌려주는 것입니다.

![화면 캡처 2024-07-28 132349](https://github.com/user-attachments/assets/47bbfd4a-77ad-4e7b-a40d-1625d43862b5)

제출해보면 맞은 걸 확인하실 수 있습니다.
