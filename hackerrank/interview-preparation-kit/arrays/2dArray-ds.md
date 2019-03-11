# [2D Arrays - DS](http://hr.gs/abbdcb)

## Problem
Given a **6 x 6** 2D Array, **arr**:
```
1 1 1 0 0 0
0 1 0 0 0 0
1 1 1 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0
```
We define an hourglass in **A** to be a subset of values with indices falling in this pattern in **arr**'s graphical representation:
```
a b c
  d
e f g
```
There are **16** hourglasses in **arr**, and an hourglass sum is the sum of an hourglass' values. Calculate the hourglass sum for every hourglass in **arr**, then print the maximum hourglass sum.

For example, given the 2D array:
```
-9 -9 -9  1 1 1 
 0 -9  0  4 3 2
-9 -9 -9  1 2 3
 0  0  8  6 6 0
 0  0  0 -2 0 0
 0  0  1  2 4 0
 ```
We calculate the following **16** hourglass values:
```
-63, -34, -9, 12, 
-10, 0, 28, 23, 
-27, -11, -2, 10, 
9, 17, 25, 18
```
Our highest hourglass value is **28** from the hourglass:
```
0 4 3
  1
8 6 6
```
**Note**: If you have already solved the Java domain's Java 2D Array challenge, you may wish to skip this challenge.

## Function Description
Complete the function hourglassSum in the editor below. It should return an integer, the maximum hourglass sum in the array.  

hourglassSum has the following parameter(s):
* arr: an array of integers

## Input Format

Each of the **6** lines of inputs **arr[i]** contains **6** space-separated integers **arr[i][j]**.

## Constraints
* ![constraints0](https://latex.codecogs.com/gif.latex?-9%20%5Cleq%20arr%5Bi%5D%5Bj%5D%20%5Cleq%209)
* ![constraints1](https://latex.codecogs.com/gif.latex?0%20%5Cleq%20i%2Cj%20%5Cleq%205)

## Output Format

Print the largest (maximum) hourglass sum found in **arr**.

## Sample Input
```
1 1 1 0 0 0
0 1 0 0 0 0
1 1 1 0 0 0
0 0 2 4 4 0
0 0 0 2 0 0
0 0 1 2 4 0
```
## Sample Output
```
19
```
## Explanation
**arr** contains the following hourglasses:
![explanation](https://s3.amazonaws.com/hr-assets/0/1534256743-35b846ad4a-hourglasssum.png)

The hourglass with the maximum sum (**19**) is:
```
2 4 4
  2
1 2 4
```

## Solution
```java
static int hourglassSum(int[][] arr) {
    int max = -63;                                                // 모래시계를 구성하는 값이 모두 -9일때 최대값이 -63이다

    int w = arr.length;                                           // 배열의 길이를 구함
    int h = arr[0].length;                                        // 배열의 높이를 구함
        
    for(int i=0; i<h-2; i++) {                                    // 모래시계는 사장 왼쪽상단의 위치로부터 
        for(int j=0; j<w-2; j++) {                                // 오른쪽으로 2 아래로 2 이동하므로 범위 제한을 둔다 (IndexOutOfBoundsException 방지)
            int count = 0;
            
            count += arr[i][j] + arr[i][j+1] + arr[i][j+2];       // 현재 위치에서 모래시계의 윗면 값의 합
            count += arr[i+1][j+1];                               // 현재 위치에서 모래시계의 중앙 값
            count += arr[i+2][j] + arr[i+2][j+1] + arr[i+2][j+2]; // 현재 위치에서 모래시계의 아랫면 값의 합
        
            if(max < count) {                                     // 최대값 비교
                max = count;
            }
        }
    }
    return max;
}
```

## Description
이버 문제를 풀때 당연히 주어지는 2차원 배열의 크기가 최소 3 x 3 (모래시계가 1개라도 존재함) 이라고 생각하고 문제를 풀
었으나  
Constraints에 보면 i,j 가 0 일수도 있으니까 for문에서 걸리기는 하겠지만 그전에 먼저 예외처리를 하는건 어떨까 라는 생각이 들은게    
![constraints1](https://latex.codecogs.com/gif.latex?0%20%5Cleq%20i%2Cj%20%5Cleq%205) 이 조건이 i와 j가 같다는 말은 아닌거 같아서 2차원 배열의 길이와 높이가 다르고 모래시계가 1개라도 존재하지 않는 상황(아래와 같은 input 일때)
```
1 1 1 1 1
2 2 2 2 2
```
위의 코드에서 에러가 발생할거다.
for문이 동작하기전에 조건을 확인하면 더 완벽할 코드가 될거 같지만
문제에서는 모래시계가 1개도 없을경우 return 값에 대한 가이드가 없으므로 위 코드를 제출한다.

* hourglass : 모래시계
