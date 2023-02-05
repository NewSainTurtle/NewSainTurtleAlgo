# bj13023 ABCDE

### 문제

1. 다음과 같은 친구 관계를 가진 사람 A, B, C, D, E의 존재 여부.
   1. A는 B와 친구다.
   2. B는 C와 친구다.
   3. C는 D와 친구다.
   4. D는 E와 친구다.



### 문제 풀이

1. 즉, depth가 5 이상인 경우.
2. 인접배열의 dfs를 통해 depth를 계산하여, 4 이상인 경우가 있으면 1 출력, 없으면 0을 출력.
3. 사람의 수 N이 최대 2000이므로 visited 배열을 2000으로 할당.
4. 일직선의 노드로 존재해야 하므로, return 시 이전 노드의 모든 방문을 false로 변경.



### 코드

```java
import java.util.*;
import java.io.*;
public class Main {
    static ArrayList<Integer>[] g;
    static boolean[] v;
    static int ans;
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        int N = Integer.parseInt(st.nextToken());
        int E = Integer.parseInt(st.nextToken());
        ans = 0;
        g = new ArrayList[N];
        for (int i = 0; i < N; i++) {
            g[i] = new ArrayList<>();
        }
        v = new boolean[2000];
        for (int i = 0; i < E; i++) {
            st = new StringTokenizer(br.readLine(), " ");
            int from = Integer.parseInt(st.nextToken());
            int to = Integer.parseInt(st.nextToken());
            g[from].add(to);
            g[to].add(from);
        }

        for (int i = 0; i < N; i++) {
            v[i] = true;
            dfs(i, 0);
            v[i] = false;
            if (ans == 1) break;
        }
        System.out.println(ans);
        br.close();
    }

    static void dfs (int i, int cnt) {
        if (cnt >= 4) {
            ans = 1;
            return;
        }
        for (int j:g[i]) {
            if (!v[j]) {
                v[j] = true;
                dfs(j, cnt+1);
                v[j] = false;
            }
        }
    }
}
```



