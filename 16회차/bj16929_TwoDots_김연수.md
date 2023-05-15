### BJ16929 TwoDots

[📁문제보기](https://www.acmicpc.net/problem/16929)

---

#### 문제풀이

1. 변수 선언

```java
  static int[] dx = { -1, 0, 1, 0 }; // 4방 탐색
  static int[] dy = { 0, 1, 0, -1 }; 
  static int N, M; // 맵 크기 N x M
  static char[][] map;
  static boolean visit[][];
  static String result = "No"; // 결과값
```

2. 처리

- map 크기만큼 반복문을 돌며 아직 방문하지 않은 점을 기준으로 사이클이 만들어지는지 dfs 탐색을 시작한다.
  - `dfs(int x, int y, char ch, int cnt, int dir)`
  - x,y : 탐색 위치
  - ch : 현재 탐색하는 색상
  - cnt : 현재 탐색 수
  - dir: 현재 탐색 방향

- 현재 탐색하는 점을 방문처리하고 4방 탐색을 한다.
  - 현재 탐색 방향을 제외하고 다음 점의 위치(`nx,ny`)를 찾는다. 
  - 다음 점이 map 범위 안에 있고 같은 색상일 경우 dfs를 반복한다.
- 만약 탐색하는 점의 갯수가 4개 이상이고 이미 방문한 점이라면 사이클이 된다는 의미이므로 result 값을 `Yes`로 저장한다.
- result 값이 Yes라면 dfs함수를 끝내고 그렇지 않다면 계속 dfs 탐색을 한다.

3. 출력

- 모든 반복이 끝나면 결과(`result`)를 출력한다.

---

#### 전체 코드

```java
import java.io.*;
import java.util.*;

public class Main {
  static int[] dx = { -1, 0, 1, 0 };
  static int[] dy = { 0, 1, 0, -1 };
  static int N, M;
  static char[][] map;
  static boolean visit[][];
  static String result = "No";

  public static void main(String[] args) throws IOException {
    // System.setIn(new FileInputStream("input.txt"));
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

    StringTokenizer st = new StringTokenizer(br.readLine(), " ");
    N = Integer.parseInt(st.nextToken());
    M = Integer.parseInt(st.nextToken());
    map = new char[N][M];
    visit = new boolean[N][M];

    for (int i = 0; i < N; i++) {
      map[i] = br.readLine().toCharArray();
    }

    for (int i = 0; i < N; i++) {
      for (int j = 0; j < M; j++) {
        if (visit[i][j])
          continue;
        dfs(i, j, map[i][j], 0, -1);
      }
    }

    System.out.print(result);
  }

  private static void dfs(int x, int y, char ch, int cnt, int dir) {
    if (result.equals("Yes"))
      return;
    if (cnt >= 4 && visit[x][y]) {
      result = "Yes";
      return;
    }

    visit[x][y] = true;

    for (int i = 0; i < 4; i++) {
      if (i == dir)
        continue;
      int nx = x + dx[i];
      int ny = y + dy[i];

      if (nx < 0 || ny < 0 || nx >= N || ny >= M || ch != map[nx][ny])
        continue;

      dfs(nx, ny, ch, cnt + 1, (i + 2) % 4);
    }
  }
}
```
