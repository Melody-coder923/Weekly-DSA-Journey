Two Sum
```
def twoSumTargert(nums, target):
    # nums 数组必须有序
    nums.sort()
    lo, hi = 0, len(nums) - 1
    res = []
    while lo < hi:
        sum = nums[lo] + nums[hi]
        left, right = nums[lo], nums[hi]
        if sum < target:
            while lo < hi and nums[lo] == left: 
                lo += 1
        elif sum > target:
            while lo < hi and nums[hi] == right: 
                hi -= 1
        else:
            res.append([left, right])
            while lo < hi and nums[lo] == left: 
                lo += 1
            while lo < hi and nums[hi] == right: 
                hi -= 1
    return res
```
Three Sum
```
class Solution:
    # 计算数组 nums 中所有和为 target 的三元组
    def threeSumTarget(self, nums, target):
        # 数组得排个序
        nums.sort()
        n = len(nums)
        res = []
        # 穷举 threeSum 的第一个数
        i = 0
        while i < n:
            # 对 target - nums[i] 计算 twoSum
            tuples = self.twoSumTarget(nums, i + 1, target - nums[i])
            # 如果存在满足条件的二元组，再加上 nums[i] 就是结果三元组
            for tuple in tuples:
                tuple.append(nums[i])
                res.append(tuple)
            # 跳过第一个数字重复的情况，否则会出现重复结果
            while i < n - 1 and nums[i] == nums[i + 1]:
                i += 1
            i += 1
        return res

    # 从 nums[start] 开始，计算有序数组 nums 中所有和为 target 的二元组
    def twoSumTarget(self, nums, start, target):
        # 左指针改为从 start 开始，其他不变
        lo = start
        hi = len(nums) - 1
        res = []
        while lo < hi:
            ...
        return res
```
Four Sum
```
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        # 数组需要排序
        nums.sort()
        n = len(nums)
        res = []
        # 穷举 fourSum 的第一个数
        for i in range(n):
            # 对 target - nums[i] 计算 threeSum
            triples = self.threeSumTarget(nums, i + 1, target - nums[i])
            # 如果存在满足条件的三元组，再加上 nums[i] 就是结果四元组
            for triple in triples:
                triple.append(nums[i])
                res.append(triple)
            # fourSum 的第一个数不能重复
            while i < n - 1 and nums[i] == nums[i + 1]: i += 1
        return res

    # 从 nums[start] 开始，计算有序数组 nums 中所有和为 target 的三元组
    def threeSumTarget(self, nums: List[int], start: int, target: int) -> List[List[int]]:
        n = len(nums)
        res = []
        # i 从 start 开始穷举，其他都不变
        for i in range(start, n):
            ...
        return res
```
100 sum
```
# 注意：调用这个函数之前一定要先给 nums 排序
# n 填写想求的是几数之和，start 从哪个索引开始计算（一般填 0），target 填想凑出的目标和
def nSumTarget(nums: List[int], n: int, start: int, target: int) -> List[List[int]]:
    sz = len(nums)
    res = []
    # 至少是 2Sum，且数组大小不应该小于 n
    if n < 2 or sz < n:
        return res
    # 2Sum 是 base case
    if n == 2:
        # 双指针那一套操作
        lo, hi = start, sz-1
        while lo < hi:
            sum = nums[lo] + nums[hi]
            left, right = nums[lo], nums[hi]
            if sum < target:
                while lo < hi and nums[lo] == left:
                    lo += 1
            elif sum > target:
                while lo < hi and nums[hi] == right:
                    hi -= 1
            else:
                res.append([left, right])
                while lo < hi and nums[lo] == left:
                    lo += 1
                while lo < hi and nums[hi] == right:
                    hi -= 1
        return res
    else:
        # n > 2 时，递归计算 (n-1)Sum 的结果
        for i in range(start, sz):
            if i > start and nums[i] == nums[i - 1]:
                # 跳过重复元素
                continue
            subs = nSumTarget(nums, n-1, i+1, target-nums[i])
            for sub in subs:
                # (n-1)Sum 加上 nums[i] 就是 nSum
                sub.append(nums[i])
                res.append(sub)
        return res
```
