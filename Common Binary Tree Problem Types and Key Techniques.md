## Common Binary Tree Problem Types and Key Techniques

| Problem Type                | Key Concepts and Techniques                      | Example LeetCode Problems            |
|----------------------------|--------------------------------------------------|--------------------------------------|
| **Recursive Traversal & Path Finding** | DFS + recursion, path tracking, backtracking         | 112. Path Sum, 113. Path Sum II       |
| **Tree Construction & Comparison**     | Build trees from preorder/inorder, check structure   | 105. Construct Binary Tree from Preorder and Inorder, 100. Same Tree |
| **Property Calculation**              | Height, number of nodes, max path sum, etc.          | 104. Maximum Depth, 543. Diameter     |
| **Subtree Detection**                 | Compare subtrees, prune branches                     | 572. Subtree of Another Tree          |
| **Binary Search Tree (BST) Operations** | Use BST ordering property for efficient operations  | 98. Validate Binary Search Tree       |
| **Level Order Traversal & Width**      | BFS using queue, serialization                       | 102. Binary Tree Level Order Traversal |
| **Path & Max Value Problems**          | Tracking paths, global state (e.g., max sum)         | 124. Binary Tree Maximum Path Sum     |

## 🔧 General Problem-Solving Patterns for Binary Trees

### 1. Understand Input, Output, and Edge Cases
- Consider edge cases like:
  - An empty tree
  - A single-node tree
  - Skewed trees (left-heavy or right-heavy)
- Confirm return types: list, integer, boolean, or tree structure?

### 2. Choose the Appropriate Traversal Strategy
- Based on the problem, decide:
  - **Preorder (Root-Left-Right)**: Good for copying or building trees
  - **Inorder (Left-Root-Right)**: Often used for BST-related problems
  - **Postorder (Left-Right-Root)**: Useful for deleting or computing bottom-up values
  - **Level-order (BFS)**: Needed when level structure matters (e.g., width, zigzag)

### 3. Recursive Template
- Clearly define:
  - The purpose of the recursive function (e.g., return type and parameters)
  - Base case (e.g., `if not node: return`)
  - What to return or accumulate from child nodes
- Optionally include helper functions for clean abstraction

### 4. Iterative Template (Stack or Queue)
- Use a stack for DFS (pre/in/postorder)
- Use a queue for BFS (level-order)
- Optionally include a visited marker (`None` or boolean) for precise control
- Maintain order of processing (e.g., push right before left)

### 5. Use Auxiliary Variables and State Management
- Common helpers:
  - `path`: List to track the current path from root to node
  - `max_val`: To store global maximum/minimum during traversal
  - `visited`: Set or flag to avoid cycles (in graph-like problems)
  - `level`: Integer to track current depth or height
- For backtracking problems, remember to:
  - Append before recursion
  - Pop after recursion

## Personal Mindset for Solving Binary Tree Problems
### 🧠 Step 1: Pick the Right Strategy

- Is this problem solvable by **traversal**?
  - → Write a `traverse(node)` function
  - → Use external variables to collect information
- Or can it be solved by **divide and conquer**?
  - → Write a `dfs(node)` function
  - → Use the **return values of left/right subtrees** to build the answer

### 🧭 Step 2: Define What Each Node Needs to Do

- What task should be done **at this node**?
- When should it be done? (Preorder, Inorder, Postorder?)
- What data should be passed down? (Path, sum, level, etc.)

### 🛠️ Step 3: Implement Using a Robust Template

- ✅ Base Case: `if not node: return ...`
- ✅ Recursion:
  - Traverse left/right
  - Or receive return values and combine
- ✅ Maintain:
  - Global state (max, min, count, etc.)
  - Local state (path, depth, visited)

### ⚠️ Step 4: Handle Edge Cases

- Null root?
- Leaf-only tree?
- Unbalanced shapes?

### 💬 Common Patterns to Recognize

| Problem Type | Solution Style | Notes |
|--------------|----------------|-------|
| Path / sum check | Traverse + path var | Track path during DFS |
| Tree diameter / max depth | Divide & conquer | Use return value from left/right |
| Level-order | BFS | Use queue and level counter |
| Build/Clone tree | Preorder | Recursively create nodes |
