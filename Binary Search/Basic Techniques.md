## Binary Search

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
def find_first_ge(nums, target):
    left, right = 0, len(nums) - 1
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] < target: #这里的符号很重要, 如果求left是第一个>target的位置,而不是本题的>=就需要修改
            left = mid + 1
        else:
            #ans = mid   第一个满足nums[mid]>=target条件的位置(过程中一直在更新),整个程序结束会=left,但是过程中left会动态变化,两个没有关系. 这里是提示过程观察调试可以用,实际代码不要写
            right = mid - 1
    # 判断是否存在目标值
    if left >= len(nums):
        return -1
    # 判断找到的左边界是否是目标值
    return left if nums[left] == target else -1   # left 就是第一个 >=target 的位置 
```

更容易理解版本,上面版本是把下面版本融合了
```
def find_first_ge(nums, target):
    left, right = 0, len(nums) - 1
    while left<=right:
        mid=left+(right-left)//2
        if nums[mid]>target:
            right=mid-1
        elif nums[mid]<target:
            left=mid+1
        else:
            right=mid-1
    if left >= len(nums) or nums[left] < target:  # 越界或找不到
        return -1
    return left
```

如果用左闭有开方法,就不需要要最后的判断部分
```
def left_bound(nums: List[int], target: int) -> int:
    left = 0
    # 注意
    right = len(nums)
    
    # 注意
    while left < right:
        mid = left + (right - left) // 2
        if nums[mid] == target:
            right = mid
        elif nums[mid] < target:
            left = mid + 1
        elif nums[mid] > target:
            # 注意
            right = mid

    return left
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
    # 判断是否存在目标值
    if right < 0 or right >= len(nums):
        return -1
    # 判断找到的右边界是否是目标值
    return right if nums[right] == target else -1  # right 就是最后一个 <= target 的位置
```

下面的写法可以整合为上面的
```
def find_last_le(nums, target):
    left,right=0, len(nums) -1
     while left <= right:
        mid = left+ (left + right) // 2
        if nums[mid]>target:
            right=mid-1
        elif nums[mid]<target:
            left=mid+1
        else:
            left=mid+1
    if right < 0 or right >= len(nums):
        return -1
    return right
```

如果写左闭右开,就不需要写最后的判断部分
```
def right_bound(nums, target):
    left, right = 0, len(nums)
    while left < right:
        mid = left + (right - left) // 2
        if nums[mid] == target:
            # 注意
            left = mid + 1
        elif nums[mid] < target:
            left = mid + 1
        elif nums[mid] > target:
            right = mid
    # 注意
    return left - 1
```
<img width="1574" height="618" alt="image" src="https://github.com/user-attachments/assets/cb87f9bf-2d8d-4072-8259-e99d15fea168" />
