## pg*다리를지나는트럭*김강호.md

https://school.programmers.co.kr/learn/courses/30/lessons/42583

---

#### 알고리즘 : 큐

---

### 풀이 과정 :

1. 다리를 큐라고 생각하고 품
2. 다리가 비어있거나, 비어있지 않지만 무게가 충분하면 큐에 현재 트럭을 넣어주면서 현재 무게와 시간을 증가시켜준다.
3. 비어있지 않지만 무게가 초과된다면 큐에 0을 넣어주고, 시간을 증가시켜준다.
4. 다리의 길이가 가득 차있다면 현재 무게에 다리의 트럭무게 만큼 빼준다.

---

### Source

```java
import java.util.*;
class Solution {
    static Queue<Integer> bridge;
    static int time, cur_weight = 0;
    public int solution(int bridge_length, int weight, int[] truck_weights) {
        int size = truck_weights.length;
        time = bridge_length;
        bridge = new ArrayDeque<>();
        for(int i=0; i<size; i++) {
            while(true) {
                if(bridge.size()==bridge_length) cur_weight -= bridge.poll();
                else if(bridge.isEmpty()) {
                    over(truck_weights[i]);
                    break;
                }
                else {
                    if(cur_weight + truck_weights[i] <= weight) {
                        over(truck_weights[i]);
                        break;
                    }
                    else {
                        bridge.add(0);
                        time++;
                    }
                }
            }
        }
        return time;
    }
    static void over(int n) {
        bridge.offer(n);
        cur_weight += n;
        time++;
    }
}
```
