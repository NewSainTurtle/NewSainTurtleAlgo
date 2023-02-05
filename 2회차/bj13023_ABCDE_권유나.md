## [😎](https://www.acmicpc.net/problem/13023) [bj13023] ABCDE

> **소요 시간: 66분<br>
> 메모리: 13060KB<br>
> 시간: 232ms**

## 문제 접근

- 사람수 최대 2000명, 친구관계 최대 2000개
- 인접 행렬을 사용할 경우보다 인접 리스트를 사용할 경우 시간 복잡도가 줄어든다

## 문제 풀이

1. 리스트를 사용해 친구 관계를 표시한다. i와 j가 친구일 경우라면 relation i번째에 j를 넣고, relation j번째에 i를 넣는다

2. visit에는 방문한 사람 인덱스를 넣는다. ABCDE 관계만 알면 되므로 크기는 5로 정의한다.

3. 0부터 N전까지 순차적으로 접근하면서 해당 사람을 A로 지정한다.

4. A 친구가 1명이라도 있다면 find함수를 실행한다. (5-7)

5. ABCDE관계를 찾았으면 true를 반환한다.(idx가 5일때)

6. 이전 사람의 친구 관계 리스트를 가져와 순차적으로 접근한다.<br>
   6-1. 친구가 visit에 있는 사람인지 확인하고 있다면 다음 친구를 확인한다.<br>
   6-2. 친구가 visit에 없는 사람이라면 친구를 visit에 추가하고 find함수를 호출한다.<br>
   6-3. find함수 반환값이 true라면 true를 리턴한다.<br>

7. 반복문이 종료됐는데 함수가 종료되지 않았다면 false를 리턴한다.

8. find함수가 true를 반환했다면, ABCDE 관계가 존재하므로 answer를 1로 변경하고 반복문을 종료한다.

9. answer를 출력한다

## 전체 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.List;
import java.util.StringTokenizer;

public class Main_bj13023 {

    static int[] visit;
    static List<Integer>[] relation;
    static int N, M;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        relation = new List[N];
        visit = new int[5];

        int i, j, answer = 0;

        for (int m = 0; m < M; m++) {
            st = new StringTokenizer(br.readLine(), " ");
            i = Integer.parseInt(st.nextToken());
            j = Integer.parseInt(st.nextToken());
            if (relation[i] == null) {
                relation[i] = new ArrayList<>();
            }
            if (relation[j] == null) {
                relation[j] = new ArrayList<>();
            }
            relation[i].add(j);
            relation[j].add(i);
        }

        for (int n = 0; n < N; n++) {
            visit[0] = n;
            if (relation[n] != null && find(1)) {
                answer = 1;
                break;
            }
        }
        System.out.print(answer);
        br.close();
    }

    static boolean find(int idx) {
        if (idx == 5) {
            return true;
        }
        List<Integer> list = relation[visit[idx - 1]];
        check:
        for (int i = 0; i < list.size(); i++) {
            visit[idx] = list.get(i);
            for (int j = 0; j < idx; j++) {
                if (visit[idx] == visit[j]) {
                    continue check;
                }
            }
            if (find(idx + 1)) {
                return true;
            }
        }
        return false;
    }
}
```
