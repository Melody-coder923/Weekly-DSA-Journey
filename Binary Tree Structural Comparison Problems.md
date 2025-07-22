# 🌲 Binary Tree Structural Comparison Problems

This note summarizes key binary tree problems related to structure comparison, such as checking symmetry, equality, and inversion.

## 📋 Table of Contents

1. [Is Same Tree (LeetCode 100)](#is-same-tree)
2. [Is Symmetric Tree (LeetCode 101)](#is-symmetric-tree)
3. [Invert Binary Tree (LeetCode 226)](#invert-binary-tree)

## 1. Is Same Tree

**LeetCode 100 - Is Same Tree**

Determine if two binary trees are structurally identical and have the same node values.

### 🔑 Key Points

- Compare two trees: `p` and `q`
- Must match **structure** and **node values**

### ✅ Recursive Solution

```python
def isSameTree(p, q):
    if not p and not q:
        return True
    if not p or not q or p.val != q.val:
        return False
    return isSameTree(p.left, q.left) and isSameTree(p.right, q.right)
```
## 2. Is Symmetric Tree

**LeetCode 101 - Is Symmetric Tree**

Determine if a binary tree is symmetric around its center (i.e., a mirror of itself).

### 🔍 Problem Description

A binary tree is symmetric if the left subtree is a mirror reflection of the right subtree.

### 🔑 Key Logic

- Compare `left` and `right` subtrees in a **mirrored** way.
- Use recursion or a queue (BFS).
- At each level, check:
  - `left.left` == `right.right`
  - `left.right` == `right.left

### ✅ Recursive DFS Solution
```python
def isSymmetric(root):
    def isMirror(p, q):
        if not p and not q:
            return True
        if not p or not q or p.val != q.val:
            return False
        return isMirror(p.left, q.right) and isMirror(p.right, q.left)

    return isMirror(root.left, root.right) if root else True
```
### 🔁 Iterative BFS Solution (Queue)
```
from collections import deque

def isSymmetric(root):
    if not root:
        return True
    queue = deque([(root.left, root.right)])
    while queue:
        left, right = queue.popleft()
        if not left and not right:
            continue
        if not left or not right or left.val != right.val:
            return False
        queue.append((left.left, right.right))
        queue.append((left.right, right.left))
    return True
```
## 3. Invert Binary Tree

**LeetCode 226 - Invert Binary Tree**

Flip a binary tree: make the left child become the right child and vice versa.

### 🔍 Problem Description

Given the root of a binary tree, invert it so that the left and right children of all nodes are swapped.

### 🔑 Key Idea

- Swap the `left` and `right` children of each node.
- Recursively or iteratively traverse the tree and apply the swap.
- This is a classic post-order problem: invert left and right first, then swap.

### ✅ Recursive DFS Solution
```python
def invertTree(root):
    if not root:
        return None
    # Recursively invert left and right subtrees
    left = invertTree(root.left)
    right = invertTree(root.right)
    # Swap them
    root.left, root.right = right, left
    return root
```
### 🔁 Iterative BFS Solution (Queue)
```python
from collections import deque

def invertTree(root):
    if not root:
        return None
    queue = deque([root])
    while queue:
        node = queue.popleft()
        # Swap children
        node.left, node.right = node.right, node.left
        if node.left:
            queue.append(node.left)
        if node.right:
            queue.append(node.right)
    return root
```




