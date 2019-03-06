# [Jumping on the Clouds](http://hr.gs/efaabf)

## Problem
Emma is playing a new mobile game that starts with consecutively numbered clouds. Some of the clouds are thunderheads and others are cumulus.
She can jump on any cumulus cloud having a number that is equal to the number of the current cloud plus **1** or **2**.
She must avoid the thunderheads. Determine the minimum number of jumps it will take Emma to jump from her starting postion to the last cloud.
It is always possible to win the game.

For each game, Emma will get an array of clouds numbered **0** if they are safe or **1** if they must be avoided.
For example, **c = [0,1,0,0,0,1,0]** indexed from **0...6**. The number on each cloud is its index in the list so she must avoid the clouds at indexes **1** and **5**.
She could follow the following two paths: **0 -> 2 -> 4 -> 6** or **0 -> 2 -> 3 -> 4 -> 6**. The first path takes **3** jumps while the second takes **4**.

## Function Description
Complete the jumpingOnClouds function in the editor below. It should return the minimum number of jumps required, as an integer.
jumpingOnClouds has the following parameter(s):
* c: an array of binary integers

## Input Format
The first line contains an integer , the total number of clouds. The second line contains  space-separated binary integers describing clouds ![img](https://latex.codecogs.com/gif.latex?c%5Bi%5D) where ![img](https://latex.codecogs.com/gif.latex?0%20%5Cleq%20i%20%3C%20n).

## Constraints
* ![constraints0](https://latex.codecogs.com/gif.latex?2%20%5Cleq%20n%20%5Cleq%20100)
* ![constraints1](https://latex.codecogs.com/gif.latex?c%5Bi%5D%20%5Cin%20%7B0%2C1%7D)
* ![constraints2](https://latex.codecogs.com/gif.latex?c%5B0%5D%20%3D%20c%5Bn-1%5D%20%3D%200)

## Output Format
Print the minimum number of jumps needed to win the game.

## Sample Input 0
```
7
0 0 1 0 0 1 0
```

## Sample Output 0
```
4
```

## Explanation 0: 
Emma must avoid **c[2]** and **c[5]**. She can win the game with a minimum of **4** jumps:  
![sample0](https://s3.amazonaws.com/hr-challenge-images/20832/1461134731-c258160d15-jump2.png)

## Sample Input 1
```
6
0 0 0 0 1 0
```

## Sample Output 1
```
3
```

## Explanation 1: 
The only thundercloud to avoid is **c[4]**. Emma can win the game in **3** jumps:  
![sample1](https://s3.amazonaws.com/hr-challenge-images/20832/1461136358-764298d363-jump5.png)

## Solution
```java
static int jumpingOnClouds(int[] c) {
    int jumpCnt = 0;
    int arrSize = c.length;
    
    for (int i = 0; i < arrSize-1; i++) {
        jumpCnt++;
        if (i<arrSize-2 && c[i+2]==0) {
            i++;
        }
    }

    return jumpCnt;
}
```

## Description
해당 문제는 풀지 못해서 Discussion의 내용을 보고 해결했는데  
원인은 피해야하는 구름과, 2칸씩 점프할 수 있는 조건을 모두 확인하려고 하니 문제가 복잡해 졌는데

단순하게 생각해서 아래와 같이 생각했으면 금방 풀었을거 같다
* 모든 구름을 1칸씩 점프한다
* 현재 위치(i)에서 2칸 뒤에 위치한 구름의 값을 확인해서 값이 0일때 (이동할 수 있을때) 1칸 더 점프한다

피해야하는 구름 체크하고, 2칸식 점프하는 조건 체크하고 하는것보다 위에 조건처럼
기본적으로 1칸씩 이동하고, 1칸을 더 이동할 수 있는 조건을 확인하는 방식이 훨씬더 문제를 간단하게 해결할 수 있다.