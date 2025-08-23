class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        if len(nums1)>len(nums2):
            nums1,nums2=nums2,nums1
        m, n = len(nums1), len(nums2)
        totalleft= (m+n+1)//2
        left1,right1=0,m
        while left1<=right1:
            # mid1 是在 nums1 中左半部分包含的元素个数（不是下标！）
            mid1=left1+(right1-left1)//2
            # mid2 是在 nums2 中左半部分包含的元素个数 (不是下标!)
            mid2=totalleft-mid1
#划分线其实是“落在两个数之间的缝隙里”，你可以理解成一个数组长度为 n，会有 n+1 个“缝隙”,取的是划分线两侧相邻的数
# 要保证 nums1[mid1 - 1] <= nums2[mid2]  and  nums2[mid2 - 1] <= nums1[mid1]
            nums1LeftMax = float('-inf') if mid1 == 0 else nums1[mid1 - 1]
            nums1RightMin = float('inf') if mid1 == len(nums1) else nums1[mid1]
            nums2LeftMax = float('-inf') if mid2 == 0 else nums2[mid2 - 1]
            nums2RightMin = float('inf') if mid2 == len(nums2) else nums2[mid2]
            if nums1LeftMax <= nums2RightMin and nums2LeftMax <= nums1RightMin:
                if (m+n)%2!=0:
                    return max(nums1LeftMax,nums2LeftMax)
                else:
                    return (max(nums1LeftMax,nums2LeftMax)+min(nums1RightMin,nums2RightMin))/2
            elif nums1LeftMax > nums2RightMin:
                right1 = mid1  # move left
            else:
                left1 = mid1 + 1  # move right
