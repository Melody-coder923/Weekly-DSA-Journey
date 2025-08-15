LC70  climbing stairs

Recursion+Memo
```
def climbStairs(self, n: int) -> int:
    """
    :param 参数名: 参数的含义
    :return: 返回值的含义
    """
        memo = {}
        def dfs(rest):
            if rest < 0:
                return 0
            if rest == 0:
                return 1
            if rest in memo:
                return memo[rest]
            memo[rest] = dfs(rest - 1) + dfs(rest - 2)
            return memo[rest]
        return dfs(n)
```
DP

```
class Solution:
    def climbStairs(self, n: int) -> int:
        if n <= 1:
            return 1
        dp = [0] * (n + 1)
        dp[0]=1
        dp[1]=1
        for i in range(2, n + 1):
            dp[i] = dp[i - 1] + dp[i - 2]
        return dp[n]
```
