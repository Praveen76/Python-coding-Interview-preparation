# Q1. Implement linear search to find an item.

Ans:

```python

def linear_search(nums, item):
    
    for i in range(len(nums)):
        if nums[i] == item:
            return i
    
    return -1


nums = [1, 5, -3, 10, 55, 100]
print(linear_search(nums, 10))

```

# Q 1.1: Implement Linear search using recursion to find an item from the list.
Ans:

```python
def recursive_linear_search(nums, item, index=0):
 
    # Base case: When item is not present in the list
    if index >= len(nums):
        return -1
 
    # Base case: When item if found in the list
    if nums[index] == item:
        return index
    
    # Keep searching for item recursively
    return recursive_linear_search(nums, item, index+1)
 
 
nums = [1, 4, 6, -4, 0, 100]
print(recursive_linear_search(nums, 0))
```