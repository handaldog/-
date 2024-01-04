# 4️⃣0️⃣ [프로그래머스] 기지국 설치 </span> 

---
### 📃 문제 설명
N개의 아파트가 일렬로 쭉 늘어서 있습니다. 이 중에서 일부 아파트 옥상에는 4g 기지국이 설치되어 있습니다. 기술이 발전해 5g 수요가 높아져 4g 기지국을 5g 기지국으로 바꾸려 합니다. 
그런데 5g 기지국은 4g 기지국보다 전달 범위가 좁아, 4g 기지국을 5g 기지국으로 바꾸면 어떤 아파트에는 전파가 도달하지 않습니다.

예를 들어 11개의 아파트가 쭉 늘어서 있고, [4, 11] 번째 아파트 옥상에는 4g 기지국이 설치되어 있습니다. 
만약 이 4g 기지국이 전파 도달 거리가 1인 5g 기지국으로 바뀔 경우 모든 아파트에 전파를 전달할 수 없습니다. 
(전파의 도달 거리가 W일 땐, 기지국이 설치된 아파트를 기준으로 전파를 양쪽으로 W만큼 전달할 수 있습니다.)

![image](https://github.com/handaldog/DailyAlgo/assets/96431408/ac96c5f6-f0a5-42c8-ada9-f61165da5cae)

이때, 우리는 5g 기지국을 최소로 설치하면서 모든 아파트에 전파를 전달하려고 합니다. 위의 예시에선 최소 3개의 아파트 옥상에 기지국을 설치해야 모든 아파트에 전파를 전달할 수 있습니다.

아파트의 개수 N, 현재 기지국이 설치된 아파트의 번호가 담긴 1차원 배열 stations, 전파의 도달 거리 W가 매개변수로 주어질 때, 
모든 아파트에 전파를 전달하기 위해 증설해야 할 기지국 개수의 최솟값을 리턴하는 solution 함수를 완성해주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/ec653a6e-c06e-4bc9-b967-030ac287a176)


---
### ❗️ 풀이 
1. 기준점(center)을 하나 잡는다. -> 아주 초기에는 1이다. 아파트는 1부터 시작하니깐.
2. stations를 돌면서 그 안에 추가 기지국을 세주고 for문이 끝나도 아파트가 남아있다면 추가적으로 더해줘야 한다.
3. stations에서는 이미 설치된 포인트의 최소값과 현재 기준점을 비교한다. (최소값 > center , 최소값 == center, 최소값 < center)
4. 최소값 > center 일때는 (최대값+w) - (w*2+1) - center + 1 / w*2+1 로 나눴을때 나머지가 나오는 지 안나오는 지 확인해서 따로 계산해 줘야한다.
5. stations이 끝났음에도 아파트가 남아있는지 확인 후, 남아있다면 w*2+1로 나눴을때 나머지가 나오는 지 안나오는지 확인해서 계산한다.


--- 
### 👨‍💻 배운 점
1. 오랜만에 머리를 굴려서 재밌었다.
2. 끝까지 풀어서 해결한 것이 뿌듯했다.

---
### 💰 코드
```
class Solution {
    public int solution(int n, int[] stations, int w) {
        
        int answer = 0;
        
        int size = (w*2)+1;

        int center = 1;
        
        for(int i=0;i<stations.length;i++){
            int min = stations[i] - w;
            
            // 최소값 > center
            if(min > center){
                int check = ((((stations[i] + w) - size)-center) +1);
                if(check%size == 0){
                answer += check/size;
            }
                else {
                    answer+= (check/size)+1;
                 }
               center = stations[i] +w +1;
            }
            
            // 최소값 < center
            else if(min <= center)center = stations[i] +w +1;
            
        }
        
        // 원래 기지국을 다 해결했는데도 남아있는 아파트가 있다면
        if(center < n){
           
            if((n-center)%size == 0){
                answer += (n-center)/size;
            }
            else {
               answer+= ((n-center)/size)+1;
            }
            
        }
        else if(center == n){
            answer++;
        }
        
        
        return answer;
    }
}

```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/b1f7e7f1-7867-42c1-9821-09d8e087615a)

