# [bj13023] ABCDE

๐[๋ฌธ์  ๋ฐ๋ก๊ฐ๊ธฐ](https://www.acmicpc.net/problem/13023)



---

### ๋ฌธ์  ํ์ด

1. ์ฌ๋ ์ N๊ณผ ์น๊ตฌ ๊ด๊ณ ์ M์ ์๋ ฅ๋ฐ๋๋ค.
2. ๋ฆฌ์คํธ ๋ฐฐ์ด์ ์น๊ตฌ ๊ด๊ณ๋ฅผ ๋ฃ์ด์ค๋ค.
3. `A๋ E์ ์น๊ตฌ๋ค` ๊ด๊ณ๊ฐ ์กด์ฌํ๋์ง์ ๊ฐ์ ์๋ฏธ์ด๋ฏ๋ก ๊น์ด๊ฐ 5์ธ dfs ๊ทธ๋ํ์ธ์ง๋ฅผ ํ์ธํด๋ณธ๋ค.
4. dfs ์๊ณ ๋ฆฌ์ฆ์ ์ด์ฉํ์ฌ ๊น์ด๊ฐ 5์ธ์ง๋ฅผ ํ์ธํ๊ณ  5์ผ ๊ฒฝ์ฐ 1, ์๋ ๊ฒฝ์ฐ 0์ ์ถ๋ ฅํ๋ค.



-----

### ์์ค ์ฝ๋

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
		
		for(int i=0; i<N; i++) { // ์น๊ตฌ ๊ด๊ณ๊ฐ ์กด์ฌํ๋ฉด ์ข๋ฃ
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

