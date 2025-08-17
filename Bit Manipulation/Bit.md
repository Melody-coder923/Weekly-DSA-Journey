231. Power of Two
```
class Solution:
    def isPowerOfTwo(self, n: int) -> bool:
        return n > 0 and (n & (n - 1)) == 0
```
✳️ 例子 1：n = 8
n      = 1000
n - 1  = 0111
         ----
n & n-1 = 0000 ✅

✳️ 例子 2：n = 6 （不是 2 的幂）
n      = 0110
n - 1  = 0101
         ----
n & n-1 = 0100 ❌

🔑 所以结论是：
如果 n 是 2 的幂 → 它的二进制只有一个 1 → n & (n - 1) == 0
如果 n 不是 2 的幂 → 二进制里有多个 1 → 结果不为 0
