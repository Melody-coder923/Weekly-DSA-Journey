# Binary Tree Structure and Traversal Methods

## 1. TreeNode Definition

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

## 2. Tree Traversal Types
| Traversal Type           | Recursive | Iterative (Stack) | BFS (Queue) |
| ------------------------ | --------- | ----------------- | ----------- |
| Preorder (Root → L → R)  | ✅         | ✅                 | ❌           |
| Inorder (L → Root → R)   | ✅         | ✅                 | ❌           |
| Postorder (L → R → Root) | ✅         | ✅                 | ❌           |
| Level Order (BFS)        | ❌         | ❌                 | ✅           |

## 3. Recursive Solutions

### 3.1 Preorder Traversal

```python
# Leetcode 144. Binary Tree Preorder Traversal
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res = []
        def dfs(node):
            if node is None:
                return
            res.append(node.val)
            dfs(node.left)
            dfs(node.right)
        dfs(root)
        return res
```
### 3.2 Inorder Traversal

```python
# Leetcode 94. Binary Tree Inorder Traversal
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res=[]
        def dfs(node):
            if node is None:
                return
            dfs(node.left)
            res.append(node.val)
            dfs(node.right)
        dfs(root)
        return res
```
### 3.3 Postorder Traversal

```python
# Leetcode 145. Binary Tree Postorder Traversal
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res=[]
        def dfs(node):
            if node is None:
                return
            dfs(node.left)
            dfs(node.right)
            res.append(node.val)
        dfs(root)
        return res
```
## 4. Iterative Solutions (Stack)

### 4.1 Preorder Traversal
```python
# Leetcode 144. Binary Tree Preorder Traversal
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []
        res = []
        stack = [root]
        while stack:
            node = stack.pop()
            res.append(node.val)
            if node.right:
                stack.append(node.right)
            if node.left:
                stack.append(node.left)
        return res
```
### 4.2 Inorder Traversal
```python
# Leetcode 94. Binary Tree Inorder Traversal
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res = []
        stack = []
        cur = root
        while cur or stack: #It can handle empty tree situation
            # Step 1: Go as left as possible
            while cur:
                stack.append(cur)
                cur = cur.left
            # Step 2:Once the leftmost node is reached, begin processing the top node from the stack
            cur = stack.pop()
            res.append(cur.val)
            # Step 3: Move to right subtree
            cur = cur.right
        return res
```
### 4.3 Postorder Traversal
```python
# Leetcode 145. Binary Tree Postorder Traversal
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []
        stack = [root]
        result = []
        while stack:
            node = stack.pop()
            # Step 1: Visit the current node
            # This follows a modified preorder pattern: root → right → left
            result.append(node.val)
            # Step 2: Push left and right children onto the stack
            # Left child is pushed first so that the right child is processed before it
            if node.left:
                stack.append(node.left)
            # Push right child later so it's processed before left
            if node.right:
                stack.append(node.right)
        # Step 3: Reverse the result to convert it to postorder: left → right → root
        return result[::-1]
```
### 4.4 Unified Iterative Method for Preorder, Inorder, and Postorder Traversal
When traversing a binary tree, the act of **visiting a node** (i.e., traversing it) and **processing a node** (i.e., adding its value to the result) are often not aligned in time.

To handle this, we can push both the nodes to be visited and the nodes ready to be processed onto the stack, but we need a way to **mark** nodes that are ready for processing.

There are two common marking methods:

- **Method 1: Null Pointer Marking**
  After pushing a node onto the stack, immediately push a `None` (null pointer) as a marker. When the `None` is encountered during popping, it signals that the next node popped is ready to be processed. This technique is called the **null pointer marking method**.

- **Method 2: Boolean Flag Marking**
  Instead of a separate marker, pair each node with a boolean flag. The flag `False` (default) indicates the node is being visited for the first time and its children need to be arranged on the stack. The flag `True` means the node’s position has been arranged previously and it is now ready for processing. This is called the **boolean flag marking method**.

Both approaches enable clear differentiation between the two stages — traversal and processing — ensuring correct iterative tree traversal logic.
#### Method 1: Null Pointer Marking
```python
class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        result = []
        stack = []
        if root:
            stack.append(root)
        while stack:
            node = stack.pop()
            if node is not None:
                # Push right child first (to be processed later)
                if node.right:
                    stack.append(node.right)
                # Push left child next (to be processed first)
                if node.left:
                    stack.append(node.left)
                # Push current node and a None marker to indicate it has been visited
                stack.append(node)
                stack.append(None)
            else:
                # When None is encountered, pop the next node and add its value to result
                node = stack.pop()
                result.append(node.val)
        return result
```
```python
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        result = []
        stack = []
        if root:
            stack.append(root)

        while stack:
            node = stack.pop()
            if node is not None:
                # Push right child first (if exists)
                if node.right:
                    stack.append(node.right)
                # Push current node and a None marker to indicate this node is visited but not processed yet
                stack.append(node)
                stack.append(None)
                # Push left child last (so it is processed first)
                if node.left:
                    stack.append(node.left)
            else:
                # When None marker is encountered, pop next node and add its value to result
                node = stack.pop()
                result.append(node.val)
        return result
```
```python
class Solution:
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        result = []
        stack = []
        if root:
            stack.append(root)

        while stack:
            node = stack.pop()
            if node is not None:
                # Push current node and a None marker indicating it has been visited but not processed
                stack.append(node)
                stack.append(None)
                # Push right child first (to be processed after left child)
                if node.right:
                    stack.append(node.right)
                # Push left child last (to be processed first)
                if node.left:
                    stack.append(node.left)
            else:
                # When None marker is encountered, pop the node and add its value to result
                node = stack.pop()
                result.append(node.val)
        return result
```
#### Method 2: Boolean Flag Marking
```python
class Solution:
    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        values = []
        stack = [(root, False)] if root else []  # (node, visited) tuple; visited indicates if node has been processed

        while stack:
            node, visited = stack.pop()

            if visited:
                # Node is revisited after its children have been processed
                values.append(node.val)
                continue

            # First time visit:
            # Postorder: left -> right -> node
            # So push node back with visited=True, then right and left children
            stack.append((node, True))  # Mark node as visited for future processing

            if node.right:
                stack.append((node.right, False))  # Right child pushed before left

            if node.left:
                stack.append((node.left, False))  # Left child pushed last to be processed first

        return values
```
## 5. BFS (Breadth-First Search)
### 5.1 Length method (Iterative BFS):
Use a queue and loop through current level's node count.
```
# Leetcode 102. Binary Tree Level Order Traversal
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []

        queue = collections.deque([root])  # Initialize queue with root node
        result = []

        while queue:
            level = []
            level_length = len(queue)  # Number of nodes at current level

            # Iterate over all nodes in the current level
            for _ in range(level_length):
                node = queue.popleft()
                level.append(node.val)

                # Add left child if it exists
                if node.left:
                    queue.append(node.left)
                # Add right child if it exists
                if node.right:
                    queue.append(node.right)

            result.append(level)  # Append current level's values to result

        return result
```
### 5.2 Recursive method:
Use recursion with level parameter to group nodes by depth.
```
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []

        levels = []

        def traverse(node: Optional[TreeNode], level: int) -> None:
            if not node:
                return

            # If this is the first time we reach this level, create a new list
            if len(levels) == level:
                levels.append([])

            # Append current node's value to the corresponding level list
            levels[level].append(node.val)

            # Recurse for left and right children, increase level by 1
            traverse(node.left, level + 1)
            traverse(node.right, level + 1)

        traverse(root, 0)
        return levels
```



