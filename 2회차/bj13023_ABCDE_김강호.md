# ๐ 13023 (ABCDE)

## ์์์๊ฐ, ๋ฉ๋ชจ๋ฆฌ

160ms, 16676KB

## ํ์ด ๋ฐฉ๋ฒ

- 2์ฐจ์ ๋ฐฐ์ด์ ์ฌ์ฉํ์ฌ ์๋ ฅ๊ฐ์ ๋ฐ์์ ํ์๋๋ฐ ์๊ฐ์ด๊ณผ ๋ฐ์.
- ArrayList๋ฅผ ์ฌ์ฉํ์ฌ ํด๊ฒฐ.
  - 2์ฐจ์๋ฐฐ์ด์ ์ฐ๊ฒฐ๋์ง ์์ ๋ถ๋ถ๊น์ง ํ์ํ๋ฏ๋ก ์ต๋๋ก N-1๋ฒ์ฉ N๋ฒ ํ์ํ๊ฒ๋จ.
  - ArrayList๋ฅผ ์ฌ์ฉํ๋ฉด ์ฐ๊ฒฐ๋ ๋ถ๋ถ๋ง ํ์ํ  ์ ์์.
- Class๋ฅผ ๋ง๋ค์ด ์ฐ๊ฒฐ๋ Node๋ฅผ ์ง์  ๊ฐ์ง๊ณ  ์๊ฒ ํ์ฌ ์๊ฐ์ ๋ ๋จ์ถ์ํฌ ์ ์์์.

## Code

```Java
import java.io.*;
import java.util.*;
public class Main {
    static class Node {
        int v;
        Node n;
        public Node(int v,Node n) {
            this.v = v;
            this.n =n;
        }
    }
    static Node[] node;
    static boolean[] v;
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());
        node = new Node[N];
        for(int i=0; i<M; i++) {
            st = new StringTokenizer(br.readLine()," ");
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            node[a] = new Node(b,node[a]);
            node[b] = new Node(a,node[b]);
        }
        for(int i=0; i<N; i++) {
            v = new boolean[N];
            if(dfs(i,0)) {
                System.out.println(1);
                return;
            }
        }
        System.out.println(0);
        br.close();
    }
    static boolean dfs(int x, int cnt) {
        if(cnt==4) return true;
        v[x] = true;
        for(Node temp = node[x]; temp!=null; temp=temp.n) {
            if(!v[temp.v]) {
                if(dfs(temp.v,cnt+1)) return true;
            }
        }
        v[x] = false;
        return false;
    }
}
```
