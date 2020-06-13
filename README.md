# Daily Temperatures
## https://leetcode.com/problems/daily-temperatures


### Implementation : Naive
```java
class Solution {
    public int[] dailyTemperatures(int[] T) {
        if(T == null || T.length == 0)
            return T;
        
        for(int i = 0; i < T.length; i++) {
            int daysToWait = 1;
            boolean warmerDay = false;
            for(int j = i + 1; j < T.length; j++) {
                if(T[j] > T[i]) {
                    warmerDay = true;
                    T[i] = daysToWait;
                    break;
                }
                daysToWait++;
            }
            if(!warmerDay)
                T[i] = 0;
        }
        return T;
    }
}
```
