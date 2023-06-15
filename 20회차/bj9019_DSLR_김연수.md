### BJ9019 DSLR

[📁문제보기](https://www.acmicpc.net/problem/9019)

---

#### 문제풀이

1. 테스트 케이스(T) 만큼 반복한다.

2. A,B를 입력받고 A → B가 되기 까지 BFS를 통해 구해보도록 하자.

3. BFS 함수에서 사용할 변수 선언

   ```java
   Queue<Integer> que = new LinkedList<>(); 
   char[] command = new char[10000]; // 명령어 저장
   int[] from = new int[10000]; // 경로 저장
   ```

4. `que`에 시작 숫자(`A`)를 담고 탐색을 시작한다.

   - `que`에서 숫자를 하나씩 poll한 값은 현재 가르키는 값이라는 의미로 `now`라고 한다.

5. 4번의 반복으로 i의 숫자에 따라 `DSLR`명령어를 실행하고 그 결과 값을 `nx`라고 한다. 

6. `nx`가 아직 방문하지 않은 값이라면

   - `command[nx]`에 실행했던 명령어 저장
   - `from[nx]`에 현재 숫자(`now`)를 저장한다.
   - `que`에 다음 번호로 이어서 탐색 할 수 있도록 `add(nx)`한다. 

7. 만약 `nx`가 목표 값인 `B`와 같다면

   - `from`에 저장했던 경로 B → A로 역추적하면서 `command`저장했던 명령어들을 불러와 `StringBuilder`에 저장한다.
   - 이때 저장된 `StringBuilder` 명령어는 A → B 순이 아닌 B → A 값이 되는 순서이므로 `reverse()`한 값을 리턴한다.

   ```
   if (nx == B) {
     StringBuilder sb = new StringBuilder();
     int temp = b;
     while (temp != a) {
      	sb.append(command[temp]);
      	temp = from[temp];
     }
     return sb.reverse().toString();
   }
   ```

8. 모든 테스트케이스 결과값(BFS 리턴 값)을 개행문자로 구분하여 `StringBuilder`에 저장한다.

9. 모든 테스트 케이스 반복이 끝나면 StringBuilde에 저장된 값을 출력한다.

---

#### 전체 코드

```java
import java.io.*;
import java.util.*;

public class Main {
  public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    StringBuilder sb = new StringBuilder();

    int T = Integer.parseInt(br.readLine());
    while (T-- > 0) {
      StringTokenizer st = new StringTokenizer(br.readLine());
      int A = Integer.parseInt(st.nextToken());
      int B = Integer.parseInt(st.nextToken());
      sb.append(BFS(A, B)).append('\n');
    }

    System.out.print(sb);
  }

  private static String BFS(int A, int B) {
    Queue<Integer> que = new LinkedList<>();
    char[] command = new char[10000];
    int[] from = new int[10000];
    que.offer(A);

    while (!que.isEmpty()) {
      int now = que.poll();
      for (int i = 0; i < 4; i++) {
        int nx = calcN(i, now);
        if (command[nx] == 0) {
          command[nx] = i == 0 ? 'D' : i == 1 ? 'S' : i == 2 ? 'L' : 'R';
          from[nx] = now;
          que.add(nx);
        }
        if (nx == B) {
          StringBuilder sb = new StringBuilder();
          int temp = B;
          while (temp != A) {
            sb.append(command[temp]);
            temp = from[temp];
          }
          return sb.reverse().toString();
        }
      }
    }

    return null;
  }

  private static int calcN(int i, int now) {
    if (i == 0)
      return (2 * now) % 10000;
    if (i == 1)
      return (now == 0) ? 9999 : now - 1;
    if (i == 2)
      return (now % 1000) * 10 + now / 1000;
    return (now % 10) * 1000 + now / 10;
  }
}
```
