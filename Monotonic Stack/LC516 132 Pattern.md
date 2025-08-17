# Monotonic Stack (Summary)

## What is a Monotonic Stack?

A monotonic stack is a stack that maintains its elements in a specific order:
- **Monotonic increasing stack**: elements from bottom to top are increasing
- **Monotonic decreasing stack**: elements from bottom to top are decreasing

Used for:
- Finding the next greater/smaller element
- Range problems
- Pattern matching (like 132 pattern)

---

## Core Operations

1. **Traverse the array (usually left-to-right or right-to-left)**
2. **Maintain stack order**:
   - For increasing stack: pop when current > stack top
   - For decreasing stack: pop when current < stack top
3. **Push current element onto stack**

---

## Common Use Cases

- Next Greater Element
- Histogram (Largest Rectangle)
- Daily Temperatures
- 132 Pattern
- Sliding Window Maximum

---

## Time Complexity

- **O(n)**: Each element is pushed and popped at most once

---

## Key Properties

- Stack is used to keep potential candidates
- Helps in removing unnecessary comparisons
- Efficient for problems involving local minima/maxima or range dominance

---

LC516 132 Pattern

```
class Solution:
    def find132pattern(self, nums: List[int]) -> bool:
        stack = []
        second = float('-inf')  # nums[k]

        for i in range(len(nums) - 1, -1, -1):
            if nums[i] < second:
                return True
            while stack and nums[i] > stack[-1]:
                second = stack.pop()
            stack.append(nums[i])
        
        return False
```

