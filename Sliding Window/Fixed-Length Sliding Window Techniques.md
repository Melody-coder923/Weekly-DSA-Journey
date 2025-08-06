# Fixed-Length Sliding Window Techniques

## 1. Core Logic
> **Left subtract, right add** → Keep the window size fixed and update the state in O(1) time.
- **Right enter**: Check if `s[right]` meets the condition; if yes, increment count.
- **Left exit**: Check if `s[right - k]` meets the condition; if yes, decrement count.
- **Update result**: Maintain the maximum, minimum, or current count.

**Formula Template**:

```python
count += condition(new_right)   # Add from the right
count -= condition(old_left)    # Remove from the left
res = max(res, count)           # or min(...)
```

## 2. Initialization Technique
Use sum() + condition expression for quick initial count:
```
count = sum(c in vowels for c in s[:k])
```
- c in vowels → returns True/False
- sum() interprets True as 1 and False as 0
- Shorter and cleaner than a manual loop.

## 3. Pruning Optimization
If the result reaches the maximum possible value, return early:

```
if res == k:
    return k
```

**When applicable:**
- Maximum vowels count: theoretical upper bound = k
- Maximum sum: can precompute upper boun


LC 1456. Maximum Number of Vowels in a Substring of Given Length
```
class Solution:
    def maxVowels(self, s: str, k: int) -> int:
        vowels = set("aeiou")
        count = sum(c in vowels for c in s[:k])
        res = count
        for i in range(k, len(s)):
            count += (s[i] in vowels) - (s[i-k] in vowels)
            res = max(res, count)
            if res == k:
                return k
        return res
```

## 4. Common Scenarios
- Counting vowels in a fixed-size substring (LeetCode 1456)
- Maximum average or sum of fixed-size subarray (LeetCode 643)
- Minimum operations in fixed-size block (LeetCode 2379)
- Counting elements that meet a property (e.g., distinct characters, even numbers)

## 5. Applicability Conditions

- Fixed window size (k is constant)  
- Statistic is incrementally updatable:  
  - Boolean count  
  - Sum  
  - Frequency map updates  
- Does not require complex order-dependent operations  
  (For max/min in the window → use monotonic queue or heap instead)  

---

## 6. Thinking Framework

- Does the problem define a fixed length *k*?  
- Can the statistic be updated incrementally instead of re-checking the whole window?  
- Can the first window's value be computed in O(k)?  
- Can early termination (pruning) be applied?  
