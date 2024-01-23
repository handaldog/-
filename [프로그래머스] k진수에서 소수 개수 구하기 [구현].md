# 6️⃣4️⃣ [프로그래머스] k진수에서 소수 개수 구하기 </span> 

---
### 📃 문제 설명
양의 정수 n이 주어집니다. 이 숫자를 k진수로 바꿨을 때, 변환된 수 안에 아래 조건에 맞는 소수(Prime number)가 몇 개인지 알아보려 합니다.

0P0처럼 소수 양쪽에 0이 있는 경우
P0처럼 소수 오른쪽에만 0이 있고 왼쪽에는 아무것도 없는 경우
0P처럼 소수 왼쪽에만 0이 있고 오른쪽에는 아무것도 없는 경우
P처럼 소수 양쪽에 아무것도 없는 경우
단, P는 각 자릿수에 0을 포함하지 않는 소수입니다.
예를 들어, 101은 P가 될 수 없습니다.
예를 들어, 437674을 3진수로 바꾸면 211020101011입니다. 여기서 찾을 수 있는 조건에 맞는 소수는 왼쪽부터 순서대로 211, 2, 11이 있으며, 총 3개입니다. 
(211, 2, 11을 k진법으로 보았을 때가 아닌, 10진법으로 보았을 때 소수여야 한다는 점에 주의합니다.) 211은 P0 형태에서 찾을 수 있으며, 2는 0P0에서, 11은 0P에서 찾을 수 있습니다.

정수 n과 k가 매개변수로 주어집니다. n을 k진수로 바꿨을 때, 변환된 수 안에서 찾을 수 있는 위 조건에 맞는 소수의 개수를 return 하도록 solution 함수를 완성해 주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/409e474c-323f-472d-b6b5-ccf9a3182990)


---
### ❗️ 풀이 
1. 우선 k진수로 바꿔준다. (Integer.toString(n,k)) 사용
2. 0을 따라 나눠준다. 그러면 무조건 하나 조건이 걸리기 때문. (이건 다른사람 풀이 참고)
3. 나눴는데도 word 길이가 0이면 숫자가 한개라는 뜻. 이것만 소수인지 판별해서 0 ,1 출력한다.
4. 아니면 word를 돌면서 ""인 거 제외하고, 소수인지 판별해준다. 그리고 answer++


--- 
### 👨‍💻 배운 점
1. 진수를 자유자재로 바꾸는 법 -> Integer.toString(바꿀 숫자, 진수);
2. 문자열을 Long 으로 바꾸는 법 -> Long num = Long.parseLong(str);
---
### 💰 코드
```
import java.util.*;

class Solution {
    public int solution(int n, int k) {
        int answer = 0;
        int cnt = 0;
        // 진수로 바꾸는 법.
        String number = Integer.toString(n,k);
        
        String word[]  = number.split("0");
        
        System.out.println("1 : " + word.length);
        
        if(word.length == 0){
            Long longnumber = Long.parseLong(number);
            for(int j=1;j<=Math.sqrt(longnumber);j++){
                if(longnumber%j == 0){
                    cnt++;
                }
            }
            if(cnt == 1){
                return 1;
            }
            else{
                return 0;
            }
        }
        
        for(int i=0;i<word.length;i++){
            cnt = 0;
            
            if(word[i].equals(""))continue;
            Long num = Long.parseLong(word[i]);
            
            for(int j=1;j<=Math.sqrt(num);j++){
                if(num%j == 0 && num > 1){
                    cnt++;
                }
            }
            if(cnt == 1){
                answer++;
            }
        }
    
           
        return answer;
    }
}

```
