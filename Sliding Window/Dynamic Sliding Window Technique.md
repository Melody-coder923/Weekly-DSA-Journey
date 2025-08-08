# Dynamic Sliding Window Core Idea

- Both pointers, `left` and `right`, move flexibly based on conditions.  
- The window size is not fixed and can expand or shrink dynamically.  
- The goal is to find the optimal sub-interval (subarray or substring) that satisfies certain conditions, such as containing specific characters or having a sum meeting a threshold.

Leetcode 76
```
def min_window(s, t):
    from collections import Counter
    need = Counter(t)
    window = Counter()
    have, need_count = 0, len(need)
    left = 0
    res = float('inf'), None, None  # 窗口大小，左边界，右边界

    for right, c in enumerate(s):
        window[c] += 1
        if c in need and window[c] == need[c]:
            have += 1
        
        # 收缩窗口，直到不满足覆盖条件
        while have == need_count:
            # 更新结果
            if right - left + 1 < res[0]:
                res = (right - left + 1, left, right)

            # 移出左边元素，缩小窗口
            window[s[left]] -= 1
            if s[left] in need and window[s[left]] < need[s[left]]:
                have -= 1
            left += 1

    return "" if res[0] == float('inf') else s[res[1]:res[2]+1]
```
