560. Subarray Sum Equals K

```
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        count = defaultdict(int)
        count[0] = 1 
        currSum = 0
        res = 0
        for num in nums:
            currSum += num
            if currSum - k in count:
                res += count[currSum - k]
            count[currSum] += 1
        return res
```
