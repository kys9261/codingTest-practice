# [New Year Chaos](http://hr.gs/fccdad)

## Problem
It's New Year's Day and everyone's in line for the Wonderland rollercoaster ride! There are a number of people queued up, and each person wears a sticker indicating their initial position in the queue. Initial positions increment by **1** from **1** at the front of the line to at the back.

Any person in the queue can bribe the person directly in front of them to swap positions. If two people swap positions, they still wear the same sticker denoting their original places in line. One person can bribe at most two others. For example, if and **Person 5** bribes **Person 4**, the queue will look like this: **1,2,3,4,5,6,7,8**.

Fascinated by this chaotic queue, you decide you must know the minimum number of bribes that took place to get the queue into its current state!

## Function Description

Complete the function minimumBribes in the editor below. It must print an integer representing the minimum number of bribes necessary, or ```Too chaotic``` if the line configuration is not possible.
minimumBribes has the following parameter(s):
* q: an array of integers

## Input Format

The first line contains an integer **t**, the number of test cases.
Each of the next **t** pairs of lines are as follows: 
- The first line contains an integer **t**, the number of people in the queue 
- The second line has  space-separated integers describing the final state of the queue.

## Constraints
* ![constraints0](https://latex.codecogs.com/gif.latex?1%20%5Cleq%20t%20%5Cleq%2010)
* ![constraints0](https://latex.codecogs.com/gif.latex?1%20%5Cleq%20n%20%5Cleq%2010^5)

## Subtasks
For **60%** score ![subtasks0](https://latex.codecogs.com/gif.latex?1%20%5Cleq%20n%20%5Cleq%2010^3)  
For **100%** score ![subtasks1](https://latex.codecogs.com/gif.latex?1%20%5Cleq%20n%20%5Cleq%2010^5)

## Output Format
Print an integer denoting the minimum number of bribes needed to get the queue into its final state. Print ```Too chaotic``` if the state is invalid, i.e. it requires a person to have bribed more than **2** people.

## Sample Input
```
2
5
2 1 5 3 4
5
2 5 1 3 4
```

## Sample Output
```
3
Too chaotic
```

## Explanation
## Test Case 1

The initial state:  
![testcase0](https://s3.amazonaws.com/hr-challenge-images/494/1451665589-31d436ba19-pic11.png)  
After person **5** moves one position ahead by bribing person **4**:
![testcase1](https://s3.amazonaws.com/hr-challenge-images/494/1451665679-6504422ed9-pic2.png)  
Now person **5** moves another position ahead by bribing person **3**:
![testcase2](https://s3.amazonaws.com/hr-challenge-images/494/1451665818-27bd62bb0d-pic3.png)  
And person **2** moves one position ahead by bribing person **1**:
![testcase3](https://s3.amazonaws.com/hr-challenge-images/494/1451666025-02a2395a00-pic5.png)  
So the final state is **2,1,5,3,4** after three bribing operations.

## Test Case 2
No person can bribe more than two people, so its not possible to achieve the input state.

## Solution
```java
static void minimumBribes(int[] q) {
    int bribesCnt = 0;
    
    for(int i = q.length-1; i >= 0; i--) {             // 배열의 뒤부터 확인
        if(q[i] != (i+1)){                             // 배열의 값이 원래 위치에 있지 않을 경우만 확인
            if((i-1 >= 0) && q[i-1] == (i+1)) {        // i-1이 0 이상 (out of index) && 원래 있어야할 위치보다 1칸 앞에 있음
                int tmp = q[i-1];                      // swap(q[i-1], q[i])
                q[i-1] = q[i];
                q[i] = tmp;

                bribesCnt++;                          
            } else if((i-2 >= 0) && q[i-2] == (i+1)) { // i-2이 0 이상 (out of index) && 원래 있어야할 위치보다 2칸 앞에 있음
                q[i-2] = q[i-1];                       // 맨 앞칸과 두번째 칸을 한칸씩 뒤로 미루고
                q[i-1] = q[i];                         // 맨 앞쪽에 원래 값을 넣음
                q[i] = i+1;

                bribesCnt += 2;     
            } else {                                   // 위 두 조건에 해당하지 않을때는 프로그램 종료
                System.out.println("Too chaotic");
                return;
            }
        }
    }
    System.out.println(bribesCnt);
}
```

## Description
처음에는 되게 쉽게 생각하고 아래와 같이 문제를 풀었다.

* 원래 위치에서 2를 초과하는 위지로 이동한 값이 1개라도 존재하는지 확인 -> 'Too chaotic' 출력
* 배열 q를 정 위치로 정렬하면서 1번 정렬할때마다 카운팅

기본적으로 주어지는 입력값은 모두 만족해서 제출을 눌렀으나 일부 테스트 케이스에서 Timeout에러가 발생하였다.
배열 q를 정 위치로 이동하면서 단순히 반복문 2개를 이용해서 정렬을 하다보니 시간복잡도가 O(N^2)이 되었던게 문제였던거 같다

고민을 해도 쉽게 문제가 풀리지 않아서 Editorial의 설명과 코드를 보았는데 의외로 문제가 쉽게 풀렸다. 
간단하게 생각해서 사람이 원래 위치에 있지 않을때, 현재 위치의 1칸 앞 또는 2칸 앞이 원래 위치인지 확인해 이동하고 그 외의 경우엔 프로그램을 종료 처리하면 되었다.

예를들어 **[2, 1, 5, 4, 3]** 이렇게 input값이 들어오면 아래 순서로 진행된다.
1. 배열의 맨 끝(q[4])의 원래 값은 5이고, 원래 위치는 두칸앞 q[2]번 이므로 (q[idx-2] == idx+1)  
q[3]은 q[2]로, q[4]는 q[3]으로 한칸씩 앞으로 당겨주고 [q]4에는 원래값 5를 넣어주면 된다.  
**[2, 1, 5, 4, 3] -> [2, 1, 4, 3, 5]**

2. 배열의 q[3]의 원래값은 4 이고, 한칸앞 q[2]에 위치하므로 q[3]과 q[2]의 위치를 바꿔준다. (q[idx-1] == idx+1)  
**[2, 1, 4, 3, 5] -> [2, 1, 3, 4, 5]**
3. 배열의 q[2]의 원래값은 3이고 원래 자리에 위치하므로 넘어간다.

4. 배열의 q[1]의 원래값은 2이고, 한칸앞 q[0]에 위치하므로 q[1]과 q[1]의 위치를 바꿔준다. (q[idx-1] == idx+1)  
**[2, 1, 4, 3, 5] -> [1, 2, 3, 4, 5]**
