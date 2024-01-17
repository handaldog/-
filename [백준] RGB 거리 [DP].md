# 4️⃣6️⃣ [백준] RGB 거리 </span> 

---
### 📃 문제 설명
RGB거리에는 집이 N개 있다. 거리는 선분으로 나타낼 수 있고, 1번 집부터 N번 집이 순서대로 있다.

집은 빨강, 초록, 파랑 중 하나의 색으로 칠해야 한다. 
각각의 집을 빨강, 초록, 파랑으로 칠하는 비용이 주어졌을 때, 아래 규칙을 만족하면서 모든 집을 칠하는 비용의 최솟값을 구해보자.

1번 집의 색은 2번 집의 색과 같지 않아야 한다.
N번 집의 색은 N-1번 집의 색과 같지 않아야 한다.
i(2 ≤ i ≤ N-1)번 집의 색은 i-1번, i+1번 집의 색과 같지 않아야 한다.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/f63b8768-e306-49bb-90d6-d48474b7b594)


---
### ❗️ 풀이 
1. 따로 값을 저장해 둘 2차원배열도 따로 만들어놓는다.
2. for문을 돌면서 자기 자신과 같은 열이면 continue 했다.
3. 그리고 따로 만들어 둔 2차원배열에 저장해두고
4. 비교하면서 최소값을 찾아냈다.


--- 
### 👨‍💻 배운 점
1. Arrays.fill() -> 2차원 배열을 채울땐 좀 다름.

---
### 💰 코드
```

import java.util.*;

public class RGB거리 {

	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		
		int n  = sc.nextInt();
		
		long min = 100000000;
		
		long house[][] = new long[n][3];
		
		long check[][] = new long [n][3];
		
		for(int i=0;i<n;i++) {
			Arrays.fill(check[i], 100000000);
		}
		
		
		for(int i=0;i<n;i++) {
			for(int j=0;j<3;j++) {
				house[i][j] = sc.nextInt();
			}
		}
		
		for(int i=0;i<n-1;i++) {
			for(int j=0;j<3;j++) {
				for(int k=0;k<3;k++) {
					if(j==k)continue;
					check[i+1][k] = Math.min(house[i][j] + house[i+1][k], check[i+1][k]);
				}
			}
			for(int h=0;h<3;h++) {
				house[i+1][h] = check[i+1][h];
			}
			
		}
		
		for(int i=0;i<3;i++) {
			min = Math.min(house[n-1][i], min);
		}
		
		System.out.println(min);

	}

}


```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/8bfa52fb-6c53-4569-a06f-01abdcfbca08)
