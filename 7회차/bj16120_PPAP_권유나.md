## [🍎🖋🍍](https://www.acmicpc.net/problem/16120) [bj16120] PPAP

> **소요 시간: 17분<br>
> 메모리: 24424KB<br>
> 시간: 176ms**

## 문제 접근

- ⚠️ 주의: P는 PPAP 문자열이다.
- PPAP 문자열 중 A만 하나이므로 A를 기준으로 PPAP 문자열인지 확인한다.
- 인덱스 포인터를 이용해 PPAP를 P로 변환한다.
- PPAP 문자열이라면 answer에는 P만 저장되어야한다.

## 문제 풀이

1. 입력문자열을 문자형 배열로 변환해 input에 저장한다.

2. input을 순차접근하면서 PPAP 문자열인지 확인한다.

3. answer[idx]에 input[i]를 저장하고 answer[idx]가 A인지 확인한다.

4. A라면 input[i+1]와 직전에 answer에 저장된 2개의 문자가 P인지 확인한다. 맞다면 idx를 2 줄이고, i를 1 증가시킨다. 그리고 3번으로 돌아간다.

5. idx를 1 증가시킨다.

6. answer에 저장된 문자가 P인경우 PPAP를 출력한다. 아니라면 NP를 출력한다.

## 전체 코드

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class Main_bj16120 {

    public static void main(String args[]) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        char[] input = br.readLine().toCharArray();
        char[] answer = new char[input.length];
        int idx = 0;
        for (int i = 0; i < input.length; i++) {
            answer[idx] = input[i];
            if (idx >= 2 && i < input.length - 1 && answer[idx] == 'A') {
                if (input[i + 1] == 'P' && answer[idx - 1] == 'P' && answer[idx - 2] == 'P') {
                    idx -= 2;
                    i++;
                } else {
                    break;
                }
            }
            idx++;
        }
        if (idx == 1 && answer[0] == 'P') {
            System.out.println("PPAP");
        } else {
            System.out.println("NP");
        }
    }
}
```
