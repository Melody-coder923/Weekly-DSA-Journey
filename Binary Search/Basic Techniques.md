#Binary Search
while left<=right 
```
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1  # Not found
```

upper_bound(nums, target)
```
def find_first_gt(nums, target):
    left, right = 0, len(nums) - 1
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] < target: #这里的符号很重要, 如果求left是第一个>target的位置,而不是本题的>=就需要修改
            left = mid + 1
        else:
            #ans = mid   第一个满足nums[mid]>=target条件的位置(过程中一直在更新),整个程序结束会=left,但是过程中left会动态变化,两个没有关系. 这里是提示过程观察调试可以用,实际代码不要写
            right = mid - 1
    return left  # left 就是第一个 >=target 的位置 
```

lower_bound(nums, target)
```
def find_last_le(nums, target):
    left, right = 0, len(nums) - 1
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] <= target:
            #ans = mid   最后一个满足nums[mid] <= target条件的位置(过程中一直在更新),整个程序结束会=right,但是过程中right会动态变化,两个没有关系. 这里是提示过程观察调试可以用,实际代码不要写
            left = mid + 1 #这里的符号很重要, 如果求right是最后一个<target的位置,而不是本题的<=就需要修改
        else:
            right = mid - 1
    return right  # right 就是最后一个 <= target 的位置
```
<img width="1574" height="618" alt="image" src="https://github.com/user-attachments/assets/cb87f9bf-2d8d-4072-8259-e99d15fea168" />
