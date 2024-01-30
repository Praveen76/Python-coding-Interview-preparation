# Q1. Implement a binary search algorithm for a given item in a sorted list. The function should return the item's index if it is in the list. If the item is not found, the function should return -1.

Ans:

```python
def binary_search(nums, item, left_idx, right_idx):
    
    if right_idx < left_idx:
        return -1
    
    # Partition
    middle_idx = (left_idx + right_idx)//2
    
    if nums[middle_idx] == item: # item found
        return middle_idx
    elif nums[middle_idx] > item:  # discard right_nums 
        return binary_search(nums, item, left_idx, middle_idx-1)
    elif nums[middle_idx] < item:  # discard left_nums 
        return binary_search(nums, item, middle_idx+1, right_idx)
    

nums = [-5, -4, 0, 2, 4, 6, 8, 100, 500]
print(binary_search(nums, 2, 0, len(nums)-1))

```
# Q2. Implement the merge sort algorithm to sort a list of integers. The function should recursively divide the input list into halves until each sub list contains only one element. Afterwards, it should merge the sorted sub-lists to produce the final sorted list.

```python
def merge_sort(nums):
    if len(nums) == 1:
        return
    # Divide Phase
    middle_idx = len(nums)//2
    
    left_half = nums[:middle_idx]
    right_half = nums[middle_idx:]
    
    merge_sort(left_half)
    merge_sort(right_half)
    
    # Conquer Phase
    i, j, k = 0, 0, 0
    
    while i < len(left_half) and j < len(right_half):
        if left_half[i] <= right_half[j]:
            nums[k] = left_half[i]
            i += 1
        else:
            nums[k] = right_half[j]
            j += 1
        
        k += 1
        
    while i < len(left_half):
        nums[k] = left_half[i]
        i += 1
        k += 1
        
    while j < len(right_half):
        nums[k] = right_half[j]
        j += 1
        k += 1
         
        
nums = [1, 5, -2, 0, 10, 100, 55, 12, 10, 2, -10, -3]

merge_sort(nums)
print(nums)   

```

