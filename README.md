# Daily Temperatures
## https://leetcode.com/problems/daily-temperatures

Given a list of daily temperatures T, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put 0 instead.
```
For example, given the list of temperatures T = [73, 74, 75, 71, 69, 72, 76, 73], 
your output should be [1, 1, 4, 2, 1, 1, 0, 0].
```

**Note: The length of temperatures will be in the range [1, 30000]. Each temperature will be an integer in the range [30, 100].**

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
## Implementation 2 : Using stack (Iterating from left to right)
```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        if(temperatures == null || n == 0)
        return new int[0];
        if(n == 1)
         return new int[]{0};
        Stack<Integer> stack = new Stack<>();
        int[] result = new int[n];
        for(int i = 0; i < n; i++) {
            while(!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
                int index = stack.pop();
                result[index] = i - index;
            }
            stack.push(i);
        }
        while(!stack.isEmpty()) {
            int index = stack.pop();
            result[index] = 0;
        }
        return result;
    }
}
```


