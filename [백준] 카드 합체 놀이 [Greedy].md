# 4️⃣3️⃣ [백준] 카드 합체 놀이 </span> 

---
### 📃 문제 설명
석환이는 아기다. 아기 석환이는 자연수가 쓰여져있는 카드를 갖고 다양한 놀이를 하며 노는 것을 좋아한다.
오늘 아기 석환이는 무슨 놀이를 하고 있을까? 바로 카드 합체 놀이이다!

아기 석환이는 자연수가 쓰여진 카드를 n장 갖고 있다. 처음에 i번 카드엔 ai가 쓰여있다. 카드 합체 놀이는 이 카드들을 합체하며 노는 놀이이다. 
카드 합체는 다음과 같은 과정으로 이루어진다.

x번 카드와 y번 카드를 골라 그 두 장에 쓰여진 수를 더한 값을 계산한다. (x ≠ y)
계산한 값을 x번 카드와 y번 카드 두 장 모두에 덮어 쓴다.
이 카드 합체를 총 m번 하면 놀이가 끝난다. m번의 합체를 모두 끝낸 뒤, n장의 카드에 쓰여있는 수를 모두 더한 값이 이 놀이의 점수가 된다. 
이 점수를 가장 작게 만드는 것이 놀이의 목표이다.

아기 석환이는 수학을 좋아하긴 하지만, 아직 아기이기 때문에 점수를 얼마나 작게 만들 수 있는지를 알 수는 없었다(어른 석환이는 당연히 쉽게 알 수 있다). 
그래서 문제 해결 능력이 뛰어난 여러분에게 도움을 요청했다. 만들 수 있는 가장 작은 점수를 계산하는 프로그램을 만들어보자.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/d04488ab-4403-49ca-b86a-50a68db0dfce)


---
### ❗️ 풀이 
1. 말 그대로 구현을 하면 된다.
2. 나는 구현을 두가지 방식으로 했다.
3. 하나는 우선순위 큐를 사용했고, 하나는 Arrays.sort를 사용해 구현했다.


--- 
### 👨‍💻 배운 점
1. 우선순위 큐가 Arrays.sort로 정렬하는 것보다 더 시간이 적게 걸린다.
2. 수가 크다면 Long으로 하는 것이 낫다. -> 안 그럼 계속 틀림.

---
### 💰 코드
[우선순위 큐]
```
import java.util.*;

public class Main {

	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		
		PriorityQueue<Long> pq = new PriorityQueue<>();
		
		int n = sc.nextInt();
		long m = sc.nextInt();
		
		
		for(int i=0;i<n;i++) {
			pq.offer(sc.nextLong());
		}
		
		while(m > 0) {
			
			
			long sum = pq.poll() + pq.poll();
			
			pq.offer(sum);
			pq.offer(sum);
			
			m--;
		}
		
		long answer = 0;
		
		while(!pq.isEmpty()) {
			answer+= pq.poll();
		}
			
		
		
		System.out.println(answer);
		
		
		
		

	}

}


```
[Arrays.sort 사용]
```
package 문자열;

import java.util.*;

public class 카드합체놀이 {

	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		
//		PriorityQueue<Long> pq = new PriorityQueue<>();
		
		int n = sc.nextInt();
		long m = sc.nextInt();
		
		Long arr[] = new Long[n];
		
		for(int i=0;i<n;i++) {
			arr[i] = sc.nextLong();
		}
		
		while(m > 0) {
			
			Arrays.sort(arr);
			
			long sum = arr[0] + arr[1];
			
			arr[0] = arr[1] = sum;
			
			m--;
		}
		
		long answer = 0;
		
		for(int i=0;i<n;i++) {
			answer+= arr[i];
		}
			
		System.out.println(answer);
		
	}

}

```
#### 시간이 확실이 우선순위 큐 사용했을 때가 적게 걸린다.
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/e6d2b0fc-583f-4621-af9c-b03a2079d7c0)

