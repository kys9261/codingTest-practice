# [Arrays: Left Rotation](http://hr.gs/16xx)

## Problem
Check out the resources on the page's right side to learn more about arrays.  
The video tutorial is by Gayle Laakmann McDowell, author of the best-selling interview book Cracking the Coding Interview.

A left rotation operation on an array shifts each of the array's elements **1** unit to the left.  
For example, if **2** left rotations are performed on array **[1,2,3,4,5]**, then the array would become **[3,4,5,1,2]**.

Given an array **a** of **n** integers and a number, **d**, perform **d** left rotations on the array.  
Return the updated array to be printed as a single line of space-separated integers.

## Function Description
Complete the function rotLeft in the editor below. It should return the resulting array of integers.  

rotLeft has the following parameter(s):  
* An array of integers **a**.
* An integer **d**, the number of rotations.

## Input Format
The first line contains two space-separated integers **n** and **d**, the size of **a** and the number of left rotations you must perform. 
The second line contains **n** space-separated integers **a[i]**.

## Constraints
* ![constraints0](https://latex.codecogs.com/gif.latex?1%20%5Cleq%20n%20%5Cleq%2010%5E5)
* ![constraints1](https://latex.codecogs.com/gif.latex?1%20%5Cleq%20d%20%5Cleq%20n)
* ![constraints2](https://latex.codecogs.com/gif.latex?1%20%5Cleq%20a%5Bi%5D%20%5Cleq%2010%5E6)

## Output Format
Print a single line of **n** space-separated integers denoting the final state of the array after performing **d** left rotations.

## Sample Input
```
5 4
1 2 3 4 5
```

## Sample Output
```
5 1 2 3 4
```

## Explanation
When we perform **4** left rotations, the array undergoes the following sequence of changes:  
**[1,2,3,4,5] -> [2,3,4,5,1] -> [3,4,5,1,2] -> [4,5,1,2,3] -> [5,1,2,3,4]**

## Solution
```java
static int[] rotLeft(int[] a, int d) {
    int arrLength = a.length;
    int[] rotArr = new int[arrLength];
    int rotPosition = 0;                                        // a[0]의 값이 왼쪽으로 밀린 횟수 카운팅

    for(int i=d, j=0; i<arrLength; i++, j++, rotPosition++) {   // i는 a를 d만큼 왼쪽으로 이동 후 0번째 index의 값이 이동 전 배열 a에서 위치하는 index값 (설명이 좀 어려움)
        rotArr[j] = a[i];                                       // j는 aotArr의 index값 (0부터 시작)
    }

    for(int i=0; i<arrLength-rotPosition; i++) {                //rotArr에 들어가지 않은 나머지 값은 순차적으로 배열에 넣으면 됨
        rotArr[rotPosition+i] = a[i];
    }

    return rotArr;
}
```

## Description
Explanation을 보면 [1,2,3,4,5]였던 배열이 4번 왼쪽 이동해서 [5,1,2,3,4]로 된거를 확인할수 있는데  
주어진 값 d(이동할 횟수) 를 기준으로 이동 전 배열에서 index d에 해당하는 값이, 이동 후 에는 index 0 에 위치하게 된다.  

따라서 새로운 배열 rotArr에 값을 넣을때 index d 부터 배열의 끝까지 넣고 다시 index 0부터 index d 앞 까지의 값을 배열에 넣으면 된다고 생각했다.

예를들어 [1,2,3,4,5,6,7] 배열이 왼쪽으로 5 만큼 이동한 결과는 [6,7,1,2,3,4,5]
새로운 배열에 우선 [6,7] 값을 넣고 (index 5 ~ index arr.length), 다시 [1,2,3,4,5]값을 순차적으로 넣는다 (index 0 ~ index 5-1)
그러면 결과는 [6,7,1,2,3,4,5]가 된다.

** 위 코드로 문제 해결은 했으나 Editorial을 보니 문자열의 substring 처럼 배열의 특정 구간을 자르는 함수가 있는걸 알았다.(배열의 특정 구간을 잘라서 새로운 배열로 복사함)
System 클래스에 arraycopy라는 함수가 존재하고 요약하면 아래와 같다.
```java
/*
* Copies an array from the specified source array, beginning at the specified position, to the specified position of the destination array.
* 
* src: source array.
* srcPos: starting position in the source array.
* dest: destination array
* destPos: starting position in the destination array.
* length: number of array elements to be copied.
*/
void arraycopy(Object src, int srcPos, Object dest, int destPos, int length)
```

이 함수를 이용해서 구현하면
```java
System.arraycopy(a, d, rotArr, 0, arrLength - d);  //배열 a에서 index d 부터 시작하고, 배열길이에서 d를 뺀 만큼(이동되는 배열 수) rotArr 배열의 index 0 위치에 복사한다.
System.arraycopy(a, 0, rotArr, arrLength - d, d);  //배열 a에서 index 0 부터 시작하고, d까지만큼 의 배열을 rotArr배열의 index (arrLength - d) 위치에 넣는다.
```

주석 내용이 조금 이상한거 같지만 결국 내가 구현한 코드랑 비슷하게 왼쪽으로 이동되는 배열 + 오른쪽으로 이동되는 배열 이렇게 두개로 나눈걸 새로운 배열에 복사하면 된다.
System 클래스에 대해서는 한번 공부해보아야 할거 같다 arraycopy 함수가 있는걸 알았으면 더 쉽게 풀수 있었던 문제였을거 같고.

arraycopy 함수가 훨씬더 빠른 성능을 보여주는데 해당 함수에 native 키워드가 붙어있어서 당장 정확한 구현내용은 확인하기가 어려웠지만 한번 어떻게 구현되는지 궁금하다.


