# 📘 13023 (ABCDE)

## 소요시간, 메모리

160ms, 16676KB

## 풀이 방법

- 2차원 배열을 사용하여 입력값을 받아서 풀었는데 시간초과 발생.
- ArrayList를 사용하여 해결.
  - 2차원배열은 연결되지 않은 부분까지 탐색하므로 최대로 N-1번씩 N번 탐색하게됨.
  - ArrayList를 사용하면 연결된 부분만 탐색할 수 있음.
- Class를 만들어 연결된 Node를 직접 가지고 있게 하여 시간을 더 단축시킬 수 있었음.

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
