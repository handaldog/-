# 8️⃣0️⃣ [프로그래머스] 오픈채팅방 </span> 

---
### 📃 문제 설명
카카오톡 오픈채팅방에서는 친구가 아닌 사람들과 대화를 할 수 있는데, 
본래 닉네임이 아닌 가상의 닉네임을 사용하여 채팅방에 들어갈 수 있다.

신입사원인 김크루는 카카오톡 오픈 채팅방을 개설한 사람을 위해, 다양한 사람들이 들어오고, 
나가는 것을 지켜볼 수 있는 관리자창을 만들기로 했다. 채팅방에 누군가 들어오면 다음 메시지가 출력된다.

"[닉네임]님이 들어왔습니다."

채팅방에서 누군가 나가면 다음 메시지가 출력된다.

"[닉네임]님이 나갔습니다."

채팅방에서 닉네임을 변경하는 방법은 다음과 같이 두 가지이다.

채팅방을 나간 후, 새로운 닉네임으로 다시 들어간다.
채팅방에서 닉네임을 변경한다.
닉네임을 변경할 때는 기존에 채팅방에 출력되어 있던 메시지의 닉네임도 전부 변경된다.

예를 들어, 채팅방에 "Muzi"와 "Prodo"라는 닉네임을 사용하는 사람이 순서대로 들어오면 채팅방에는 다음과 같이 메시지가 출력된다.

"Muzi님이 들어왔습니다."
"Prodo님이 들어왔습니다."

채팅방에 있던 사람이 나가면 채팅방에는 다음과 같이 메시지가 남는다.

"Muzi님이 들어왔습니다."
"Prodo님이 들어왔습니다."
"Muzi님이 나갔습니다."

Muzi가 나간후 다시 들어올 때, Prodo 라는 닉네임으로 들어올 경우 기존에 채팅방에 남아있던 Muzi도 Prodo로 다음과 같이 변경된다.

"Prodo님이 들어왔습니다."
"Prodo님이 들어왔습니다."
"Prodo님이 나갔습니다."
"Prodo님이 들어왔습니다."

채팅방은 중복 닉네임을 허용하기 때문에, 현재 채팅방에는 Prodo라는 닉네임을 사용하는 사람이 두 명이 있다. 
이제, 채팅방에 두 번째로 들어왔던 Prodo가 Ryan으로 닉네임을 변경하면 채팅방 메시지는 다음과 같이 변경된다.

"Prodo님이 들어왔습니다."
"Ryan님이 들어왔습니다."
"Prodo님이 나갔습니다."
"Prodo님이 들어왔습니다."

채팅방에 들어오고 나가거나, 닉네임을 변경한 기록이 담긴 문자열 배열 record가 매개변수로 주어질 때, 
모든 기록이 처리된 후, 
최종적으로 방을 개설한 사람이 보게 되는 메시지를 문자열 배열 형태로 return 하도록 solution 함수를 완성하라.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/46a61ec7-b005-44c8-a088-101ff515934d)


---
### ❗️ 풀이 
1. 우선 map에 enter, change 일때 아이디를 키로 두고 닉네임을 값으로 두어 값을 계속 바뀌게 했다.
2. 그리고 enter나 leave의 경우에는 arraylist를 따로 만들고 door라는 클래스를 하나 만들어서
3. 지속해서 축적했다 -> 유저아이디, (enter or leave)로
4. 그리고 list에 있는 것들을 모두 빼면서 map에 마지막으로 정해진 닉네임을 빼면서 answer에 넣었다.



---
### 💰 코드
```
import java.util.*;

class Solution {
    
    static class door{
        String userid;
        String inout;
        
        door(String userid, String inout){
            this.userid = userid;
            this.inout = inout;
        }
    }
    
    public String[] solution(String[] record) {
        
        
        HashMap<String, String> nickname = new HashMap<>();
        
        ArrayList<door> list = new ArrayList<>();
        
        for(int i=0;i<record.length;i++){
            String info[] = record[i].split(" ");
            
            // System.out.println("1 : " + info[0]);
            
            if(info[0].equals("Enter")){
                if(nickname.containsKey(info[1])){
                    nickname.remove(info[1]);
                    nickname.put(info[1], info[2]);
                }
                else{
                    nickname.put(info[1], info[2]);
                }
                
                list.add(new door(info[1], info[0]));
            }
            else if (info[0].equals("Leave")){
                list.add(new door(info[1], info[0]));
            }
            else{
                nickname.remove(info[1]);
                nickname.put(info[1], info[2]);
            }
        }
        
        String[] answer = new String[list.size()];
        
        for(int i=0;i<list.size();i++){
            door dor = list.get(i);
            if(dor.inout.equals("Enter")){
              answer[i] = nickname.get(dor.userid) + "님이 들어왔습니다.";
            }
            else{
                answer[i] = nickname.get(dor.userid) + "님이 나갔습니다.";
            }
            
        }
        
        return answer;
    }
}
```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/e08889fe-2261-4e19-91b2-be543c25c5c9)

