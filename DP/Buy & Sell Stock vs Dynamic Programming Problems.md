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
