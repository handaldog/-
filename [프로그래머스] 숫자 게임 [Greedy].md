# 5️⃣6️⃣ [프로그래머스] 숫자 게임 </span> 

---
### 📃 문제 설명
xx 회사의 2xN명의 사원들은 N명씩 두 팀으로 나눠 숫자 게임을 하려고 합니다. 
두 개의 팀을 각각 A팀과 B팀이라고 하겠습니다. 숫자 게임의 규칙은 다음과 같습니다.

먼저 모든 사원이 무작위로 자연수를 하나씩 부여받습니다.
각 사원은 딱 한 번씩 경기를 합니다.
각 경기당 A팀에서 한 사원이, B팀에서 한 사원이 나와 서로의 수를 공개합니다. 그때 숫자가 큰 쪽이 승리하게 되고, 
승리한 사원이 속한 팀은 승점을 1점 얻게 됩니다.
만약 숫자가 같다면 누구도 승점을 얻지 않습니다.
전체 사원들은 우선 무작위로 자연수를 하나씩 부여받았습니다. 그다음 A팀은 빠르게 출전순서를 정했고 자신들의 출전 순서를 B팀에게 공개해버렸습니다. 
B팀은 그것을 보고 자신들의 최종 승점을 가장 높이는 방법으로 팀원들의 출전 순서를 정했습니다. 이때의 B팀이 얻는 승점을 구해주세요.
A 팀원들이 부여받은 수가 출전 순서대로 나열되어있는 배열 A와 i번째 원소가 B팀의 i번 팀원이 부여받은 수를 의미하는 배열 B가 주어질 때, 
B 팀원들이 얻을 수 있는 최대 승점을 return 하도록 solution 함수를 완성해주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/c9c2dfba-c645-4686-84cf-0ff81c4e6a2e)


---
### ❗️ 풀이 
먼저 A,B 모두 오름차순을 해준다.
1. 처음 풀이는 LinkedList에 되는 A >= 인 애들을 집어넣으면서 비교했다.
2. 비교할때는 B가 더 큰 경우에는 리스트에서 삭제해주는 방식으로 했더니 자꾸 틀렸다.
3. 그래서 답을 참고했다. https://tosuccess.tistory.com/91
4. 생각은 똑같았는데 방식이 달랐다.


--- 
### 👨‍💻 배운 점


---
### 💰 코드
[첫번째 LinkedList 사용]
```
import java.util.*;

class Solution {
    public int solution(int[] A, int[] B) {
        int answer = 0;
        
        Arrays.sort(A);
        Arrays.sort(B);
        
        LinkedList<Integer> list = new LinkedList<>();       
        
        for(int i=0;i<A.length;i++){
            if(A[i] >= B[i]){
                if(list.size() > 0){
                    if(list.get(0) < B[i]){
                        list.remove(0);
                        answer++;
                    }
                    else if(list.get(0) >= B[i]){
                       list.add(A[i]); 
                    }
                }
                else{
                    list.add(A[i]);
                }
              }
            else {
                answer++;
            }
                  
                }
        
        return answer;
    }
}

```
[두번째 답안 참고]
```
import java.util.*;

class Solution {
    public int solution(int[] A, int[] B) {
        int answer = 0;
        
        Arrays.sort(A);
        Arrays.sort(B);
        
        int index=0;
        
        for(int i=0;i<A.length;i++){
            if(A[index] >= B[i]){
               
              }
            else {
                index++;
                answer++;
            }
                  
                }
        
        return answer;
    }
}
```
