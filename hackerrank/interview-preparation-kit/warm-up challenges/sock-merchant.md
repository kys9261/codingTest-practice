
# Sock Merchant

## Problem

John works at a clothing store. He has a large pile of socks that he must pair by color for sale.
Given an array of integers representing the color of each sock, 
determine how many pairs of socks with matching colors there are **n = 7**.
For example, there are  socks with colors **ar = [1,2,1,2,1,3,2]**. There is one pair of color **1** and one of color **2**. 
There are three odd socks left, one of each color. The number of pairs is ****.

### Function Description

Complete the sockMerchant function in the editor below. 
It must return an integer representing the number of matching pairs of socks that are available.

sockMerchant has the following parameter(s):

* n: the number of socks in the pile
* ar: the colors of each sock

### Input Format

The first line contains an integer n, the number of socks represented in **ar**. 
The second line contains **n** space-separated integers describing the colors **ar[i]** of the socks in the pile.

### Constraints
* 1 <= n <= 100
* 1 <= ar[i] <= 100  where  0 <= i < n

###Output Format

Return the total number of matching pairs of socks that John can sell.

### Sample Input
```
9  
10 20 20 10 10 30 50 10 20
```
### Sample Output
```
3
```
### Explanation
![explanation](https://s3.amazonaws.com/hr-challenge-images/25168/1474122392-c7b9097430-sock.png)

### Solution
```java
static int sockMerchant(int n, int[] ar) {
    Map<Integer, Integer> map = new HashMap<>();

    for(int i=0; i<n; i++){
        Integer value = map.get(ar[i]);
        if(value == null){
            map.put(ar[i], 1);
        }else{
            map.put(ar[i], ++value);
        }
    }

    Set<Integer> entries = map.keySet();
    Iterator<Integer> i = entries.iterator();

    int cnt = 0;
    while(i.hasNext()){
       int value = map.get(i.next());
        if(value >= 2){
            cnt += value/2;
        }
    }
    return cnt;
}    
```

### Comment
input에서 각 양말이 숫자로 구분되어 있으므로
Map을 만들고 양말을 key값으로, 갯수를 value값으로 만들어서 넣는다.
반복문을 통해서 양말의 갯수가 2개(1쌍) 이상일때, 양말의 갯수를 2로 나눈 몫은 해당 양말 쌍의 갯수가 된다.
모든 양말을 체크해서 양말 쌍의 갯수를 모두 더해 return 한다.

* 참고 : 양말 쌍의 갯수를 구할때 비트연산자중 shift연산을 통해 계산해도 됨
```
cnt += value >> 1        // cnt += value/2 와 동일한 결과를 가짐
```
