# Left Insert
```
def binarySearchLeftInsert(nums, target):
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return left

```

```
def binarySearchLeftInsert(nums, target):
    left, right = 0, len(nums)  # right is set to len(nums)
    
    while left < right:  # left < right is now the condition
        mid = (left + right) // 2
        
        if nums[mid] < target:
            left = mid + 1
        else:
            right = mid
    
    return left

```

# Right Insert
```
def binarySearch(nums, target):
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if nums[mid] <= target:
            left = mid + 1
        else:
            right = mid - 1
    
    return left

```

```
def binarySearch(nums, target):
    left, right = 0, len(nums)  # right is set to len(nums)
    
    while left < right:  # left < right is now the condition
        mid = (left + right) // 2
        
        if nums[mid] <= target:
            left = mid + 1
        else:
            right = mid
    
    return left

```