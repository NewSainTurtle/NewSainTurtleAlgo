### BJ13023 ABCDE

[📁문제보기](https://www.acmicpc.net/problem/13023)

---

#### 문제풀이

1. 서로 친구일 경우 서로를 각자의 친구리스트에 저장(a 와 b가 친구 일 경우 a의 친구 리스트에 b를, b의 친구 리스트에는 a를 저장)
2. 각자의 친구 리스트를 dfs로 돌면서 ABCDE 관계가 되는지 확인
   - 현재 친구 리스트에서 방문하지 않은 친구가 있다면 그 친구의 리스트에서 이전 까지 방문하지 않은 친구가 있는지 확인(재귀 반복)
   - 5번 방문하게 된다면 ABCDE 관계이므로 result를 true, 그렇지 않으면 false 저장
3. result가 true 이면 1을 false 이라면 0을 출력한다

<img src="https://user-images.githubusercontent.com/83412032/216843337-3edb18a5-2f7d-47d2-a54d-d9ec21bdb698.jpg" alt="20230206_035909" style="zoom: 20%;" />

---

#### 전체 코드

```java
import java.io.*;
import java.util.*;

public class Main {
  static int N, M;
  static ArrayList<Integer>[] list;
  static boolean[] visit;
  static boolean result = false;

  public static void main(String[] args) throws Exception {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

    StringTokenizer st = new StringTokenizer(br.readLine());
    N = Integer.parseInt(st.nextToken()); // 사람수
    M = Integer.parseInt(st.nextToken()); // 친구 관계의 수

    list = new ArrayList[N];
    for (int i = 0; i < N; i++) list[i] = new ArrayList<Integer>();

    for (int i = 0; i < M; i++) {
      st = new StringTokenizer(br.readLine());
      int a = Integer.parseInt(st.nextToken());
      int b = Integer.parseInt(st.nextToken());
      list[a].add(b);
      list[b].add(a);
    }

    visit = new boolean[N];
    for (int i = 0; i < N; i++) {
      dfs(i, 1);
      if (result) break;
    }

    System.out.print(result ? 1 : 0);
  }

  private static void dfs(int start, int cnt) {
    if (cnt == 5) {
      result = true;
      return;
    }

    visit[start] = true;
    for (int next : list[start]) {
      if (!visit[next]) dfs(next, cnt + 1);
    }
    visit[start] = false;
  }
    
}
```

