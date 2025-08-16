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

**LC63 Unique Paths II**

Recursion+Memo
```
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        m,n=len(obstacleGrid),len(obstacleGrid[0])
        if obstacleGrid[0][0]==1 or obstacleGrid[m-1][n-1]==1:
            return 0
        memo={}
        def dfs(x,y):
            if x < 0 or y < 0:
                return 0
            if obstacleGrid[x][y] == 1:
                return 0
            if (x, y) == (0, 0):
                return 1
            if (x,y) in memo:
                return memo[(x,y)]
            memo[(x, y)] = dfs(x-1, y) + dfs(x, y-1)
            return memo[(x,y)]
        return dfs(m-1,n-1)
```
DP
```
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        m,n=len(obstacleGrid),len(obstacleGrid[0])
        dp=[[0]*n for _ in range(m)]
        
        for i in range(m):
            if obstacleGrid[i][0]==1:
                break
            dp[i][0]=1

        for j in range(n):
            if obstacleGrid[0][j]==1:
                break
            dp[0][j]=1
   
        for i in range(1,m):
            for j in range(1,n):
                if obstacleGrid[i][j]==1:
                    dp[i][j] = 0
                else:
                    dp[i][j]= dp[i-1][j]+dp[i][j-1]
        return dp[m-1][n-1]
```

**LC64 Minimum Path Sum**

Recursion+Memo
```
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        m,n=len(grid),len(grid[0])
        memo={}
        def dfs(x,y):
            if x>=m or y>=n:
                return float('inf')
            if (x, y) == (m-1, n-1):
                return grid[x][y] 
            if (x, y) in memo:
                return memo[(x, y)]     
            memo[(x, y)] = grid[x][y] + min(dfs(x+1, y), dfs(x, y+1))
            return memo[(x, y)]
        return dfs(0, 0)
```

DP
```
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        m,n=len(grid),len(grid[0])
        dp = [[0] * n for _ in range(m)]
        dp[0][0] = grid[0][0]
         # 初始化第一行
        for j in range(1, n):
            dp[0][j] = dp[0][j-1] + grid[0][j]
        # 初始化第一列
        for i in range(1, m):
            dp[i][0] = dp[i-1][0] + grid[i][0]
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])
        return dp[m-1][n-1]
```

**Leetcode 120（Triangle）**

Recursion+Memo Up-Bottom
```
class Solution:
    def minimumTotal(self, triangle: List[List[int]]) -> int:
        memo = {}
        def dfs(x, y):
            if x == len(triangle) - 1:
                return triangle[x][y]
            if (x, y) in memo:
                return memo[(x, y)]
            memo[(x, y)] = triangle[x][y] + min(dfs(x+1, y), dfs(x+1, y+1))
            return memo[(x, y)]
        return dfs(0,0)
```
DP
```
class Solution:
    def minimumTotal(self, triangle: List[List[int]]) -> int:
        n = len(triangle)

        # 从倒数第二行开始往上推
        for i in range(n - 2, -1, -1):
            for j in range(len(triangle[i])):
                triangle[i][j] += min(triangle[i+1][j], triangle[i+1][j+1])

        # 顶部元素现在是最终答案
        return triangle[0][0]
```

**LC931 Minimum Falling Path Sum**

Recursion+Memo
```
class Solution:
    def minFallingPathSum(self, matrix: List[List[int]]) -> int:
        memo = {}

        def dfs(x, y):
            if y < 0 or y >= len(matrix[0]):
                return float("inf")
            if x == len(matrix) - 1:
                return matrix[x][y]
            if (x, y) in memo:
                return memo[(x, y)]
            memo[(x, y)] = matrix[x][y] + min(
                dfs(x + 1, y),
                dfs(x + 1, y + 1),
                dfs(x + 1, y - 1)
            )
            return memo[(x, y)]

        res = []
        for y in range(len(matrix[0])):
            res.append(dfs(0, y))
        return min(res)
```

DP
```
class Solution:
    def minFallingPathSum(self, matrix: List[List[int]]) -> int:
        for i in range(len(matrix)-2, -1, -1):       # 从倒数第二行往上
            for j in range(len(matrix[0])):
                down = matrix[i+1][j]
                down_left = matrix[i+1][j-1] if j-1 >= 0 else float('inf')
                down_right = matrix[i+1][j+1] if j+1 < len(matrix[0]) else float('inf')
                matrix[i][j] += min(down, down_left, down_right)
        return min(matrix[0])
```

**LC72 Edit Distance**
Recursion+Memo
```
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        m, n = len(word1), len(word2)
        memo={}
        def dfs(i,j):
            if i == m:
                return n - j 
            if j == n:
                return m - i 
            if (i, j) in memo:
                return memo[(i, j)]
            if word1[i] == word2[j]:
                memo[(i, j)] = dfs(i + 1, j + 1)
            else:
                insert_op = 1 + dfs(i, j + 1)    # 插入word2[j]
                delete_op = 1 + dfs(i + 1, j)    # 删除word1[i]
                replace_op = 1 + dfs(i + 1, j + 1)  # 替换word1[i]为word2[j]
                memo[(i, j)] = min(insert_op, delete_op, replace_op)
            return memo[(i, j)]
        return dfs(0, 0)
```
DP
```
def minDistance(word1: str, word2: str) -> int:
    m, n = len(word1), len(word2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    # 初始化边界
    for i in range(m + 1):
        dp[i][0] = i
    for j in range(n + 1):
        dp[0][j] = j
    # 迭代计算
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if word1[i-1] == word2[j-1]:
                dp[i][j] = dp[i-1][j-1]
            else:
                dp[i][j] = 1 + min(
                    dp[i-1][j],    # 删除
                    dp[i][j-1],    # 插入
                    dp[i-1][j-1]   # 替换
                )
    return dp[m][n]
```

**LC53 Max Subarray **

Recursion+Memo
```
def maxSubArray(nums):
    memo = {}
    n = len(nums)
    
    def dfs(i):
        if i == 0:
            return nums[0]
        if i in memo:
            return memo[i]
        
        memo[i] = max(nums[i], nums[i] + dfs(i - 1))
        return memo[i]
    
    max_sum = float('-inf')
    for i in range(n):
        max_sum = max(max_sum, dfs(i))
    return max_sum
```

```
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        currentsum=maxsum=nums[0]
        for num in nums[1:]:
            if currentsum>0:
                currentsum+=num
            else:
                currentsum=num
            maxsum=max(currentsum,maxsum)
        return maxsum
```
DP
```
def maxSubArray(nums):
    n = len(nums)
    dp = [0] * n  # dp[i] 表示以 i 结尾的最大子数组和
    dp[0] = nums[0]
    max_sum = dp[0]

    for i in range(1, n):
        dp[i] = max(nums[i], dp[i - 1] + nums[i])
        max_sum = max(max_sum, dp[i])

    return max_sum
```
