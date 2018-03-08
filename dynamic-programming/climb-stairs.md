# Climb Stairs

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

简单题目，相当于fibonacci数列问题，难点就是要会思维转换，转换成为递归求解问题，多训练就可以了。每次有两种选择，两种选择之后又是各有两种选择，如此循环，正好是递归求解的问题。

写成递归程序其实非常简单，三个语句就可以：
```c
int climbStairsRecur(int n) {  
        if (n == 1) return 1;  
        if (n == 2) return 2;  
        return climbStairsRecur(n-1) + climbStairsRecur(n-2);  
    }  
```

Time Complexity: $$O(n^2)$$,Space complexity : O(n)

---
## Dynamic Programming

```cpp
int climbStairs(int n)  
    {  
        vector<int> res(n+1);  
        res[0] = 1;  
        res[1] = 1;  
        for (int i = 2; i <= n; i++)  
        {  
            res[i] = res[i-1] + res[i-2];  
        }  
        return res[n];  
    }  
```
Time Complexity: O(n),Space complexity : O(n)

