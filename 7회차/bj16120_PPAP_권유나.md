## [๐๐๐](https://www.acmicpc.net/problem/16120) [bj16120] PPAP

> **์์ ์๊ฐ: 17๋ถ<br>
> ๋ฉ๋ชจ๋ฆฌ: 24424KB<br>
> ์๊ฐ: 176ms**

## ๋ฌธ์  ์ ๊ทผ

- โ ๏ธ ์ฃผ์: P๋ PPAP ๋ฌธ์์ด์ด๋ค.
- PPAP ๋ฌธ์์ด ์ค A๋ง ํ๋์ด๋ฏ๋ก A๋ฅผ ๊ธฐ์ค์ผ๋ก PPAP ๋ฌธ์์ด์ธ์ง ํ์ธํ๋ค.
- ์ธ๋ฑ์ค ํฌ์ธํฐ๋ฅผ ์ด์ฉํด PPAP๋ฅผ P๋ก ๋ณํํ๋ค.
- PPAP ๋ฌธ์์ด์ด๋ผ๋ฉด answer์๋ P๋ง ์ ์ฅ๋์ด์ผํ๋ค.

## ๋ฌธ์  ํ์ด

1. ์๋ ฅ๋ฌธ์์ด์ ๋ฌธ์ํ ๋ฐฐ์ด๋ก ๋ณํํด input์ ์ ์ฅํ๋ค.

2. input์ ์์ฐจ์ ๊ทผํ๋ฉด์ PPAP ๋ฌธ์์ด์ธ์ง ํ์ธํ๋ค.

3. answer[idx]์ input[i]๋ฅผ ์ ์ฅํ๊ณ  answer[idx]๊ฐ A์ธ์ง ํ์ธํ๋ค.

4. A๋ผ๋ฉด input[i+1]์ ์ง์ ์ answer์ ์ ์ฅ๋ 2๊ฐ์ ๋ฌธ์๊ฐ P์ธ์ง ํ์ธํ๋ค. ๋ง๋ค๋ฉด idx๋ฅผ 2 ์ค์ด๊ณ , i๋ฅผ 1 ์ฆ๊ฐ์ํจ๋ค. ๊ทธ๋ฆฌ๊ณ  3๋ฒ์ผ๋ก ๋์๊ฐ๋ค.

5. idx๋ฅผ 1 ์ฆ๊ฐ์ํจ๋ค.

6. answer์ ์ ์ฅ๋ ๋ฌธ์๊ฐ P์ธ๊ฒฝ์ฐ PPAP๋ฅผ ์ถ๋ ฅํ๋ค. ์๋๋ผ๋ฉด NP๋ฅผ ์ถ๋ ฅํ๋ค.

## ์ ์ฒด ์ฝ๋

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
