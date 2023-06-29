### BJ5525 IOIOI

[📁문제보기](https://www.acmicpc.net/problem/5525)

---

#### 문제풀이

1. 입력받은 문자열을 한 글자씩 탐색하기 위해서 char[]로 저장한다.

2. IOI의 개수를 셀 `cnt`와 총 개수를 셀 `res` 선언 및 초기화 해준다.

3. 문자열에서 IOI 세트로 개수를 세기위해 `M-2`만큼 반복을 돌며 i, i+1, i+2 순으로 IOI가 되면 `cnt`를 1 증가시킨다.
   - 이때, 다음 IOI를 찾기 위해 IOI를 만났을 때 i++, 다음 반복문 탐색을 위해 i++를 한다. 즉, 현재 위치로부터 +2한 위치에서 IOI를 재탐색 한다.

4. IOI가 되지 않을 경우에는 `cnt`를 0으로 초기화 하여 다음 IOI를 만났을 때 개수를 셀 수 있도록 한다.

5. `cnt`의 값이 N과 같아지면 `res`값을 1 증가 시킨다.

6. 문자열 탐색이 끝나면 `res`를 출력한다.

---

#### 전체 코드

```java
import java.io.*;

public class Main {
  public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    int N = Integer.parseInt(br.readLine());
    int M = Integer.parseInt(br.readLine());
    char str[] = br.readLine().toCharArray();

    int cnt = 0, res = 0;
    for (int i = 0; i < M - 2; i++) {
      if (str[i] == 'I' && str[i + 1] == 'O' && str[i + 2] == 'I') {
        cnt++;
        i++; // 다음 'I' 위치에서 탐색
      } else
        cnt = 0; // 겹쳐지 않을 경우
      if (cnt >= N)
        res++;
    }

    System.out.print(res);
  }
}

```
