# [Repeated String](http://hr.gs/11o9)

## Problem
Lilah has a string, **s**, of lowercase English letters that she repeated infinitely many times.

Given an integer, **n**, find and print the number of letter a's in the first **n** letters of Lilah's infinite string.

For example, if the string **s = "abcac"** and **n = 10**, the substring we consider is **abcacabcac**, the first **10** characters of her infinite string. There are **4** occurrences of a in the substring.

## Function Description
Complete the repeatedString function in the editor below. It should return an integer representing the number of occurrences of a in the prefix of length **n** in the infinitely repeating string.

repeatedString has the following parameter(s):

* s: a string to repeat
* n: the number of characters to consider

## Input Format
The first line contains a single string, **s**. 
The second line contains an integer, **n**.

## Constraints
* ![constraints0](https://latex.codecogs.com/gif.latex?1%20%5Cleq%20%7Cs%7C%20%5Cleq%20100)
* ![constraints1](https://latex.codecogs.com/gif.latex?1%20%5Cleq%20n%20%5Cleq%2010%5E%7B12%7D)
* For **25%** of the test cases, ![constraints2](https://latex.codecogs.com/gif.latex?n%20%5Cleq%2010%5E%7B6%7D).

## Output Format
Print a single integer denoting the number of letter a's in the first  letters of the infinite string created by repeating **s** infinitely many times.

## Sample Input 0
```
aba
10
```

## Sample Output 0
```
7
```

## Explanation 0 
The first **n = 10** letters of the infinite string are abaabaabaa. Because there are **7** a's, we print **7** on a new line.

## Sample Input 1
```
a
1000000000000
```

## Sample Output 1
```
1000000000000
```

## Explanation 1 
Because all of the first **n = 1000000000000** letters of the infinite string are a, we print **1000000000000** on a new line.

## Solution
```java
static long repeatedString(String s, long n) {
    char[] charArr = s.toCharArray();
    int countOfA = 0;

    for(int i=0; i<charArr.length; i++){
        if(charArr[i] == 'a') countOfA++; //s에 문자 a가 몇개 있나 카운트
    }

    long repeatCnt = n / s.length();      //s가 반복될 횟수
    long substringLen = n % s.length();   //s의 길이에서 몇개까지 잘라야하는지 계산
    
    long total = 0;
    total = countOfA * repeatCnt;         //반복되는 문자열중 a의 총 갯수 계산

    for(int i=0; i<substringLen; i++){
        if(charArr[i] == 'a') total++;    //나머지 잘린 문자열에서 a의 갯수 카운트
    }
    return total;
}
```

## Description
1. 주어진 문자열에 문자 a가 몇개 들어가는지 계산  
2. 총 문자열의 길이(n)를 주어진 문자열의 길이로 나누면, 주어진 문자열이 몇번 반복되어야 하는지 알 수 있음
3. 총 문자열의 길이(n)를 주어진 문자열의 길이로 나눈 나머지는 2번에서 문자열이 반복하고 추가로 필요한 문자 갯수를 알 수 있음
4. 2번과 3번에서 나온 값으로 문자 a가 총 몇개 존재하는지 계산하면 됨