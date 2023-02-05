# [bj13023] ABCDE

📖[문제 바로가기](https://www.acmicpc.net/problem/13023)



---

### 문제 풀이

1. 사람 수 N과 친구 관계 수 M을 입력받는다.
2. 리스트 배열에 친구 관계를 넣어준다.
3. `A는 E와 친구다` 관계가 존재하는지와 같은 의미이므로 깊이가 5인 dfs 그래프인지를 확인해본다.
4. dfs 알고리즘을 이용하여 깊이가 5인지를 확인하고 5일 경우 1, 아닐 경우 0을 출력한다.



-----

### 소스 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.StringTokenizer;

public class bj13023_ABCDE {
	
	static ArrayList<Integer>[] friend;
	static boolean[] visit;
	static boolean relation;
	
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		
		int N = Integer.parseInt(st.nextToken());
		int M = Integer.parseInt(st.nextToken());
		
		visit = new boolean[N];
		
		friend = new ArrayList[N];
		for(int i=0; i<N; i++) {
			friend[i] = new ArrayList<>();
		}
		
		for(int i=0; i<M; i++) {
			st = new StringTokenizer(br.readLine());
			int m = Integer.parseInt(st.nextToken());
			int n = Integer.parseInt(st.nextToken());
			
			friend[m].add(n);
			friend[n].add(m);
		}
		
		for(int i=0; i<N; i++) { // 친구 관계가 존재하면 종료
			dfs(i, 1);
			if(relation) break;
		}
		
		if(!relation)
			System.out.println(0);
		else 
			System.out.println(1);
		
	}
	
	public static void dfs(int cnt, int depth) {
		
		if(depth == 5) {
			relation = true;
			return;
		}
		
		visit[cnt] = true;
		for(int n : friend[cnt]) {
			if(!visit[n]) dfs(n, depth+1);
		}
		
		visit[cnt] = false;
		
	}
}

```

