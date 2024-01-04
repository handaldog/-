# 3️⃣9️⃣ [프로그래머스] 단속 카메라 </span> 

---
### 📃 문제 설명

고속도로를 이동하는 모든 차량이 고속도로를 이용하면서 단속용 카메라를 한 번은 만나도록 카메라를 설치하려고 합니다.

고속도로를 이동하는 차량의 경로 routes가 매개변수로 주어질 때, 모든 차량이 한 번은 단속용 카메라를 만나도록 하려면 
최소 몇 대의 카메라를 설치해야 하는지를 return 하도록 solution 함수를 완성하세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/2fdac6aa-a7bd-4c4c-b33e-69c94c8cfd3a)


---
### ❗️ 풀이 
1. 직접 그리면서 해결방안을 찾았지만 코드로 구현할 방식을 찾지 못했다.
https://maetdori.tistory.com/entry/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%EB%8B%A8%EC%86%8D%EC%B9%B4%EB%A9%94%EB%9D%BC-JAVA
이 블로그를 참고하여 해결했다.


--- 
### 👨‍💻 배운 점
1. 그리디는 특성상 문제이해는 잘 되지만 그 문제를 어떤 방식으로 어떻게 코드로 구현해야 하는지가 안되는 문제 형식인거 같다.
2. 좀 더 연습이 필요하다는 것을 깨달았다.
#### 3. 나중에 다시 풀어 볼 문제

---
### 💰 코드
```
import java.util.*;
class Solution {
    public int solution(int[][] routes) {
        
        Arrays.sort(routes, (o1,o2) -> {
            return o1[1] - o2[1];
        });
        
        int center = routes[0][1];
        
        int answer = 1;
        
        for(int i=1;i<routes.length;i++){
            
            // 기준점으로부터 진출이 작으면 커서 그대로
            // if(center >= routes[i][1])
            // 기준점으로부터 진입은 작고 진출은 크면 커서 그대로
            // else if(center > routes[i][0] && center <= routes[i][1])
            // 기준점으로부터 진입이 크면 커서 현재 보는 차량의 진출로 커서 변경
            if(center < routes[i][0]){
                center = routes[i][1];
                answer++;
            }
        }
        
        return answer;
    }
}

```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/d2c0f3e1-9c96-4957-baee-b53800015f0e)

