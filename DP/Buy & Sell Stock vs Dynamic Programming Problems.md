# 📈 Buy & Sell Stock vs Dynamic Programming Problems (LeetCode Summary)

---

## 🧩 Dynamic Programming (DP) Basics

| Concept        | Description |
|----------------|-------------|
| **State (`dp[i]`)** | Represents a subproblem's solution (e.g. min steps, max profit, number of paths, etc.) |
| **Transition** | How to compute current state from previous states |
| **Initialization** | Set base cases for `dp` array |
| **Result** | Usually found in `dp[n]`, or `max(dp)`, etc. |

---

## 💰 Buy & Sell Stock Problems (LeetCode Patterns)

Stock problems are **state machine DP problems**, typically tracking actions across days.

### Common Elements

| Concept     | Description |
|-------------|-------------|
| **Input**   | `prices: List[int]` — stock price for each day |
| **Goal**    | Maximize profit under constraints (e.g. 1 transaction, multiple transactions, cooldown, fees, etc.) |
| **States**  | Track `buy`, `sell`, sometimes with `k` transactions or cooldown |


121. Best Time to Buy and Sell Stock
```
def maxProfit_k_1(prices: List[int]) -> int:
    n = len(prices)
    if n == 0:
        return 0
    
    dp = [[0, 0] for _ in range(n)]
    # base case: 第0天
    dp[0][0] = 0
    dp[0][1] = -prices[0]

    for i in range(1, n):
        dp[i][0] = max(dp[i-1][0], dp[i-1][1] + prices[i])
        dp[i][1] = max(dp[i-1][1], -prices[i])
    
    return dp[n-1][0]
```
122
```
class Solution:
    def maxProfit_k_inf(self, prices: List[int]) -> int:
        n = len(prices)
        if n == 0:
            return 0
        
        dp = [[0, 0] for _ in range(n)]
        # base case
        dp[0][0] = 0
        dp[0][1] = -prices[0]

        for i in range(1, n):
            dp[i][0] = max(dp[i-1][0], dp[i-1][1] + prices[i])
            dp[i][1] = max(dp[i-1][1], dp[i-1][0] - prices[i])

        return dp[n-1][0]
```

     
