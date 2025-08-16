## Declarative Top-Down Constraint Recursion 声明式、向下传约束

**Concept**  
Each recursive call declares its own constraints (e.g., `lower < node.val < upper`) that apply to itself. These constraints are passed **downward** in the recursion, and each node only needs to validate those constraints.

**Advantages**  
- **Very clear and concise**: Each node checks only its own validity against the provided bounds.  
- **Efficient**: It performs a single pass over the structure (O(n) complexity).  
- **Highly reusable**: Easily adapts to problems with similar structural constraints.

**Typical Use Case**  
Validating a binary search tree by ensuring each node satisfies `lower < node.val < upper`, with `lower` and `upper` updated as recursion goes deeper.

LC98 Validate Binary Search Tree
```
def isBST(node, lower, upper):
    if not node:
        return True

    if not (lower < node.val < upper):
        return False

    return isBST(node.left, lower, node.val) and isBST(node.right, node.val, upper)
```

我的原始版本:
```
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        minValue=float('-inf')
        maxValue=float('inf')
        def helper(node,minValue,maxValue):
            if not node:
                return True
            return minValue<node.val<maxValue and helper(node.left,minValue,node.val) and helper(node.right,node.val,maxValue)
        return helper(root,minValue,maxValue)
```

#### Backtracking Problems (e.g., N-Queens, Sudoku Solver)
In backtracking algorithms, constraints are often propagated through recursive calls to explore possible solutions. For instance, in the N-Queens problem, the algorithm recursively places queens on the board, passing down constraints to ensure no two queens threaten each other. Similarly, in Sudoku solvers, constraints are passed to ensure that each number placement adheres to Sudoku rules

Example: N-Queens Problem
```
def solve_n_queens(n):
    def is_safe(board, row, col):
        # Check if a queen can be placed at board[row][col]
        for i in range(col):
            if board[row][i] == 1:
                return False
        for i, j in zip(range(row, -1, -1), range(col, -1, -1)):
            if board[i][j] == 1:
                return False
        for i, j in zip(range(row, n, 1), range(col, -1, -1)):
            if board[i][j] == 1:
                return False
        return True

    def solve(board, col):
        if col >= n:
            return True
        for i in range(n):
            if is_safe(board, i, col):
                board[i][col] = 1
                if solve(board, col + 1):
                    return True
                board[i][col] = 0
        return False

    board = [[0 for _ in range(n)] for _ in range(n)]
    if solve(board, 0):
        return board
    else:
        return None
```

#### Constraint Satisfaction Problems (CSPs)

In CSPs, such as the Sudoku puzzle, constraints are passed down recursively to ensure that each variable assignment satisfies all constraints. The recursive function explores possible assignments, and constraints are checked at each step to prune the search space.

Example: Sudoku Solver

```
def solve_sudoku(board):
    def find_empty(board):
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] == 0:
                    return (i, j)
        return None

    def valid(board, num, pos):
        row, col = pos
        for i in range(len(board[0])):
            if board[row][i] == num and col != i:
                return False
        for i in range(len(board)):
            if board[i][col] == num and row != i:
                return False
        box_x = col // 3
        box_y = row // 3
        for i in range(box_y*3, box_y*3 + 3):
            for j in range(box_x*3, box_x*3 + 3):
                if board[i][j] == num:
                    return False
        return True

    def solve(board):
        find = find_empty(board)
        if not find:
            return True
        else:
            row, col = find
        for i in range(1, 10):
            if valid(board, i, (row, col)):
                board[row][col] = i
                if solve(board):
                    return True
                board[row][col] = 0
        return False

    solve(board)
    return board
```

#### Permutations and Combinations

Algorithms generating permutations or combinations often pass constraints down recursively to ensure that each generated sequence adheres to specific rules. For example, generating all valid permutations of a set of numbers can involve passing constraints to ensure that each permutation is unique and satisfies the desired conditions.

Example: Generating Permutations

```
def permute(nums):
    def backtrack(start):
        if start == len(nums):
            result.append(nums[:])
        for i in range(start, len(nums)):
            nums[start], nums[i] = nums[i], nums[start]
            backtrack(start + 1)
            nums[start], nums[i] = nums[i], nums[start]

    result = []
    backtrack(0)
    return result
```

#### Dynamic Programming with Constraints

In dynamic programming problems, constraints are often passed down through recursive calls to ensure that subproblems are solved optimally. For instance, in the 0/1 Knapsack problem, constraints such as weight limits are passed down to ensure that the optimal solution respects the capacity constraints.
arxiv.org

Example: 0/1 Knapsack Problem
```
def knapsack(weights, values, capacity):
    def dp(i, remaining_capacity):
        if i == len(weights) or remaining_capacity == 0:
            return 0
        if weights[i] > remaining_capacity:
            return dp(i + 1, remaining_capacity)
        return max(values[i] + dp(i + 1, remaining_capacity - weights[i]),
                   dp(i + 1, remaining_capacity))

    return dp(0, capacity)
```
