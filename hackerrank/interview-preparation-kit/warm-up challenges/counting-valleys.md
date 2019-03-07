# [Counting Valleys](http://hr.gs/3rtx )

## Problem
Gary is an avid hiker. He tracks his hikes meticulously, paying close attention to small details like topography.  
During his last hike he took exactly **n** steps. For every step he took, 
he noted if it was an uphill, **U**, or a downhill, **D** step. Gary's hikes start and end at sea level and each step up or down represents a  unit change in altitude. We define the following terms:

* A mountain is a sequence of consecutive steps above sea level, starting with a step up from sea level and ending with a step down to sea level.
* A valley is a sequence of consecutive steps below sea level, starting with a step down from sea level and ending with a step up to sea level.

Given Gary's sequence of up and down steps during his last hike, find and print the number of valleys he walked through.

For example, if Gary's path is **s = [DDYYYYDD]**, he first enters a valley **2** units deep. Then he climbs out an up onto a mountain **2** units high. Finally, he returns to sea level and ends his hike.

## Function Description
Complete the countingValleys function in the editor below. It must return an integer that denotes the number of valleys Gary traversed.

countingValleys has the following parameter(s):

* n: the number of steps Gary takes
* s: a string describing his path

## Input Format
The first line contains an integer , the number of steps in Gary's hike. 
The second line contains a single string , of  characters that describe his path.

## Constraints
* ![constraints0](https://latex.codecogs.com/gif.latex?2%20%5Cleq%20n%20%5Cleq%2010%5E6)
* ![constraints1](https://latex.codecogs.com/gif.latex?s%5Bi%5D%20%5Cin%20%5Cleft%20%5C%7B%20UD%20%5Cright%20%5C%7D)

## Output Format
Print a single integer that denotes the number of valleys Gary walked through during his hike.

## Sample Input
```
8
UDDDUDUU
```

## Sample Output
```
1
```

## Explanation
If we represent _ as sea level, a step up as /, and a step down as \, Gary's hike can be drawn as:
```
_/\      _
   \    /
    \/\/
```
He enters and leaves one valley.

## Solution
```java
static int countingValleys(int n, String s) {
    char[] steps = s.toCharArray();

    int lat = 0;
    int cnt = 0;
    for(int i=0; i<n; i++){
        if(steps[i] == 'D'){
            lat -= 1;
        }else{
            lat += 1;
        }

        if(steps[i] == 'U' && lat == 0){
            cnt = cnt+1;
        }
    }
    return cnt;
}
```

## Description
어떤 상황일때 valley라고 판단해야하는지 확인하는데 시간이 조금 걸렸다.  
-를 기준으로 내려간 후 다시 -까지 돌아오는게 1 valley 라고 판단하면 된다.  

예를들어 아래와 같은경우
```
_            _
 \          /
  \    /\/\/ 
   \/\/
```
오름과 내림이 반복되지만 모든 step이 수평선(-) 아래에서 진행되었기 때문에 위 코드(?)는 valley가 1개 존재한다 라고 보아야한다.  
그럼 valley를 카운팅 하는 조건은 아래와 같다고 생각할 수 있을거 같다.
* 올라오는 스텝이고 지평선(-)에 위치함&nbsp;&nbsp;=>&nbsp;&nbsp;steps[i].equals("U") && lat == 0

따라서 아래와 같은 로직을 코드로 작성하면 된다.
1. 모든 스텝에 대해서 현재 위치(lat)을 카운팅 하고
2. 카운팅 할때마다 위 조건을 체크해서 조건이 true일경우 valley를 카운팅