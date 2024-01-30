# Q1: Find kth smallest/ largest element in the data using Quickselect selection algorithm.

Ans:
 Method 1: Kth smallest element using Quickselect selection algorithm.

```python

import random

def swap(nums, i, j):
    nums[i], nums[j] = nums[j], nums[i]
    return nums

def qs_partition(nums, first_idx, last_idx):
    pivot_idx = random.randint(first_idx, last_idx)
    swap(nums, pivot_idx, last_idx)
    
    for i in range(first_idx, last_idx):
        if nums[i] < nums[last_idx]:  # nums[i] > nums[last_idx] : for kth largest element in the data
            swap(nums, i, first_idx)
            first_idx += 1
    
    swap(nums, first_idx, last_idx)
    
    return first_idx

def qs_selection(nums, k, first_idx=0, last_idx=None):
    if last_idx is None:
        last_idx = len(nums) - 1
    
    pivot_idx = qs_partition(nums, first_idx, last_idx)
    
    if pivot_idx > k:
        return qs_selection(nums, k, first_idx, pivot_idx - 1)
    elif pivot_idx < k:
        return qs_selection(nums, k, pivot_idx + 1, last_idx)
    else:
        return nums[pivot_idx]

nums = [1, 2, -5, 10, 100, -7, 3, 4]
k = 2  # Find the 2nd smallest element (1-indexed)

result = qs_selection(nums, k-1)  # Adjust k to be 0-indexed
print(f"The {k}nd smallest element is: {result}")

```

 2. Kth largest element in the data using Quickselect method.

Method 1:

```python

import random

def swap(nums, i, j):
    nums[i], nums[j] = nums[j], nums[i]
    return nums

def qs_partition(nums, first_idx, last_idx):
    pivot_idx = random.randint(first_idx, last_idx)
    swap(nums, pivot_idx, last_idx)
    
    for i in range(first_idx, last_idx):
        if nums[i] < nums[last_idx]:  # nums[i] > nums[last_idx] : for kth largest element in the data
            swap(nums, i, first_idx)
            first_idx += 1
    
    swap(nums, first_idx, last_idx)
    
    return first_idx

def qs_selection(nums, k, first_idx=0, last_idx=None):
    if last_idx is None:
        last_idx = len(nums) - 1
    
    pivot_idx = qs_partition(nums, first_idx, last_idx)
    
    if pivot_idx > k:
        return qs_selection(nums, k, first_idx, pivot_idx - 1)
    elif pivot_idx < k:
        return qs_selection(nums, k, pivot_idx + 1, last_idx)
    else:
        return nums[pivot_idx]

nums = [1, 2, -5, 10, 100, -7, 3, 4]
k = 2  # Find the 2nd smallest element (1-indexed)

result = qs_selection(nums, len(nums)-k  # Adjust k to be 0-indexed
print(f"The {k}nd smallest element is: {result}")

```

Method 2:

```python

import random

def swap(nums, i, j):
    nums[i], nums[j] = nums[j], nums[i]
    return nums

def qs_partition(nums, first_idx, last_idx):
    pivot_idx = random.randint(first_idx, last_idx)
    swap(nums, pivot_idx, last_idx)
    
    for i in range(first_idx, last_idx):
        if nums[i] > nums[last_idx]:
            swap(nums, i, first_idx)
            first_idx += 1
    
    swap(nums, first_idx, last_idx)
    
    return first_idx

def qs_selection(nums, k, first_idx=0, last_idx=None):
    if last_idx is None:
        last_idx = len(nums) - 1
    
    pivot_idx = qs_partition(nums, first_idx, last_idx)
    
    if pivot_idx > k:
        return qs_selection(nums, k, first_idx, pivot_idx - 1)
    elif pivot_idx < k:
        return qs_selection(nums, k, pivot_idx + 1, last_idx)
    else:
        return nums[pivot_idx]

nums = [1, 2, -5, 10, 100, -7, 3, 4]
k = 2  # Find the 2nd smallest element (1-indexed)

result = qs_selection(nums, k-1)  # Adjust k to be 0-indexed
print(f"The {k}nd smallest element is: {result}")

```

Method 2:
```python

def quickselect_search(nums, k):
    if len(nums) < k:
        return None
    pivot = nums[0]
    left = [x for x in nums if x < pivot]
    right = [x for x in nums if x > pivot]
    if len(right) == 1:
        return right[0]
    elif len(right) == 0:
        return max(left)
    else:
        return quickselect_search(right, k)

# Example usage
nums = [3, 5, 2, 8, 1, 9, 4, 7, 6]
k = 2
second_largest = quickselect_search(nums, k-1)
print(f"The second largest element in {nums} is {second_largest}")
```

# Q2. Find kth smallest/largest item using median of medians algorithm.

Ans:
 1. Kth smallest item:

```python
def median_of_medians_algo(nums, k):
    
    # Partition Phase:
    
    #  Split original data into chunks of 5 items
    chunks = [nums[i:i+5] for i in range(0, len(nums), 5)]
    
    #find medians of each of these chunks
    medians = [sorted(chunk)[len(chunk)//2 ]for chunk in chunks]
    
    # pivot_val = median(medians)
    pivot_val = sorted(medians)[len(medians)//2]
    
    # Split original data into left & right lists based on comparison with pivot_val
    left_list = [val for val in nums if val < pivot_val]
    right_list = [val for val in nums if val > pivot_val]
    
    # Selection Phase
    
    pivot_idx = len(left_list)
    
    if k < pivot_idx:  # to find kth smallest number
        return median_of_medians_algo(left_list, k)
    elif k > pivot_idx:  # to find kth largest number
        return median_of_medians_algo(right_list, k-len(left_list)-1)
    else:
        return pivot_val


nums = [1, -5, 0, 10, 15, 20, 3, -1, 21, 22, 23, 24, 25, 26, 27, 28, 29]
k = 2
print(median_of_medians_algo(nums, k-1))

```
 2. To find Kth largest item:

```python
def median_of_medians_algo(nums, k):
    
    # Partition Phase:
    
    # Split original data into chunks of 5 items
    chunks = [nums[i:i+5] for i in range(0, len(nums), 5)]
    
    # Find medians of each of these chunks
    medians = [sorted(chunk)[len(chunk)//2] for chunk in chunks]
    
    # Pivot value is the median of medians
    pivot_val = sorted(medians)[len(medians)//2]
    
    # Split original data into left & right lists based on comparison with pivot_val
    left_list = [val for val in nums if val < pivot_val]
    right_list = [val for val in nums if val > pivot_val]
    
    # Selection Phase
    pivot_idx = len(left_list)
    
    if k < pivot_idx:  # To find kth smallest number
        return median_of_medians_algo(left_list, k)
    elif k > pivot_idx:  # To find kth largest number
        return median_of_medians_algo(right_list, k - pivot_idx - 1)
    else:
        return pivot_val

nums = [1, -5, 0, 10, 15, 20, 3, -1, 21, 22, 23, 24, 25, 26, 27, 28, 29]
k = 2
print(median_of_medians_algo(nums, len(nums) - k))  # Adjust k for 1-indexing

```