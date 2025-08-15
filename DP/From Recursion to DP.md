**LC70  climbing stairs**

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
State Compression
```
    def climbStairs(self, n: int) -> int:
        if n <= 1:
            return 1
        prev, curr = 1, 1
        for i in range(2, n + 1):
            prev, curr = curr, prev + curr
        return curr
```

**LC62 Unique Paths**

Recursion+Memo
```
 def uniquePaths(self, m: int, n: int) -> int:
        memo={}
        def dfs(i,j):
        # base case：到达边界，只有一种路径（一直向下或一直向右）
            if i == 0 or j == 0:
                return 1
            if (i,j) in memo:
                return memo[(i,j)]
            memo[(i,j)] = dfs(i - 1, j) + dfs(i, j - 1)
            return memo[(i, j)]
        return dfs(m - 1, n - 1)
```

DP
```
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp=[[0]*n for _ in range(m)]
        for i in range(m):
            dp[i][0]=1
        for j in range(n):
            dp[0][j]=1
        for i in range(1,m):
            for j in range(1,n):
                dp[i][j]=dp[i-1][j]+dp[i][j-1]
        return dp[m-1][n-1]
```
