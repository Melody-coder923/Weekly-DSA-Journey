## Declarative Top-Down Constraint Recursion 声明式、向下传约束

**Concept**  
Each recursive call declares its own constraints (e.g., `lower < node.val < upper`) that apply to itself. These constraints are passed **downward** in the recursion, and each node only needs to validate those constraints.

**Advantages**  
- **Very clear and concise**: Each node checks only its own validity against the provided bounds.  
- **Efficient**: It performs a single pass over the structure (O(n) complexity).  
- **Highly reusable**: Easily adapts to problems with similar structural constraints.

**Typical Use Case**  
Validating a binary search tree by ensuring each node satisfies `lower < node.val < upper`, with `lower` and `upper` updated as recursion goes deeper.

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
