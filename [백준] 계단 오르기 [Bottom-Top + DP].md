# 5️⃣1️⃣ [백준] 계단 오르기 </span> 

---
### 📃 문제 설명
계단 오르기 게임은 계단 아래 시작점부터 계단 꼭대기에 위치한 도착점까지 가는 게임이다.
<그림 1>과 같이 각각의 계단에는 일정한 점수가 쓰여 있는데 계단을 밟으면 그 계단에 쓰여 있는 점수를 얻게 된다.
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/431a8dce-7935-4631-bd23-843d5602f888)

예를 들어 <그림 2>와 같이 시작점에서부터 첫 번째, 두 번째, 네 번째, 여섯 번째 계단을 밟아 도착점에 도달하면 총 점수는 10 + 20 + 25 + 20 = 75점이 된다.

![image](https://github.com/handaldog/DailyAlgo/assets/96431408/af25e6d4-f0e7-4ab5-8ceb-f9516364c3b3)

계단 오르는 데는 다음과 같은 규칙이 있다.

1. 계단은 한 번에 한 계단씩 또는 두 계단씩 오를 수 있다. 즉, 한 계단을 밟으면서 이어서 다음 계단이나, 다음 다음 계단으로 오를 수 있다.
2. 연속된 세 개의 계단을 모두 밟아서는 안 된다. 단, 시작점은 계단에 포함되지 않는다.
3. 마지막 도착 계단은 반드시 밟아야 한다.
4. 따라서 첫 번째 계단을 밟고 이어 두 번째 계단이나, 세 번째 계단으로 오를 수 있다. 하지만, 첫 번째 계단을 밟고 이어 네 번째 계단으로 올라가거나, 첫 번째, 두 번째, 세 번째 계단을 연속해서 모두 밟을 수는 없다.

각 계단에 쓰여 있는 점수가 주어질 때 이 게임에서 얻을 수 있는 총 점수의 최댓값을 구하는 프로그램을 작성하시오.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/95624073-b03b-4040-9438-9e912c94bd36)


---
### ❗️ 풀이 
1. 이 블로그를 참고하여 일일히 그려보며 공부하고 이해한다음 안보고 풀어봤다. -> https://st-lab.tistory.com/132
2. 어느정도 이해는 됐다.


--- 
### 👨‍💻 배운 점
1. 다시 한번 풀어봐야 할 문제

---
### 💰 코드
```

import java.util.*;

public class 계단오르기 {

	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		
		int n = sc.nextInt();
		
		int step[] = new int [n+1];
		
		int dp[] = new int [n+1];
		
		for(int i=1;i<=n;i++) {
			step[i] = sc.nextInt();
		}
		
		dp[0] = 0;
		dp[1] = step[1];
		
		if(n >= 2) {
			dp[2] = step[1] + step[2];
			
		}
		else {
			System.out.println(dp[n]);
			return;
		}
		
		
		for(int i=3;i<=n;i++) {
			dp[i] = Math.max(dp[i-2], dp[i-3] + step[i-1])+ step[i];
		}
		
		System.out.println(dp[n]);

	}

}


```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/6726c659-cb22-4053-80b0-e6de9c8c7742)
