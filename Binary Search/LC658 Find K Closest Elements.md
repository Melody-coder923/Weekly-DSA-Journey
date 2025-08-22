```
class Solution:
    def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
        left, right = 0, len(arr) - k
        while left < right:
            mid = (left + right) // 2
            # 比较窗口左边和右边谁更远离 x
            if x - arr[mid] > arr[mid + k] - x:
                # 说明更靠近 x 的窗口在右边
                left = mid + 1
            else:
                # 当前窗口更靠近 x，或一样近但数值较小，向左缩
                right = mid

        # 最终 left 是最佳窗口起点
        return arr[left:left + k]
```
