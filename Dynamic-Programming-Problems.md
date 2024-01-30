# Q1. Find the subset of numbers from a list which sum up to N.

Ans:

```python

def subset_sum(M, nums):
    
    DP = [[False for _ in range(M+1)] for _ in range(len(nums)+1)]
    
    #Initialize the first row and colum to be True
    for i in range(len(nums)+1):
        DP[i][0] = True
    
    #Construct the rest of the table
 
    for i in range(1, len(nums)+1):
        for j in range(1, M+1):
                
            if j < nums[i-1]:   # if local sum value is less than the previous item
                DP[i][j] = DP[i-1][j]  # Don't include the item
                
            else:  # if local sum value is not less than the previous item
                if DP[i-1][j]:  # If previous cell value is True
                    DP[i][j] = DP[i-1][j]
                else:
                    DP[i][j] = DP[i-1][j-nums[i-1]]

    # Get the subset values which sum upto the desired sum.
    j = M
    i = len(nums)
    while i > 0 or j > 0:

        if DP[i][j] == DP[i-1][j]:  # If current cell item is same as above cell item. 
            i = i-1
        else:
            print('item for the subset: %d' % nums[i - 1])
            j = j-nums[i-1]  # Decrement the column index by actual integer, and decrement the row index by 1.
            i = i-1
        
                
M = 12
nums = [1, 2, 4, 6]

subset_sum(M, nums)

```

# Q2. Find the longest common subsequence between two strings.
Ans:

```python
def longest_common_subseq(s1, s2):
    
    DP = [[0 for _ in range(len(s1)+1)] for _ in range(len(s2)+1)]

    for i in range(len(s1)):
        DP[i][0] = 0

    # Construct the table
    for i in range(1, len(s1)+1):
        for j in range(1, len(s2)+1):
            
            if s1[i-1] == s2[j-1]: # if chars are matching
                DP[i][j] = DP[i-1][j-1]+1
            else:  
                DP[i][j] = max(DP[i-1][j], DP[i][j-1])
                
    # Retrieve the longest common subsequence
    lcs = ''
    i, j = len(s1), len(s2)
    
    while i > 0 or j > 0:
        if s1[i-1] == s2[j-1]:  # if chars are matching then char is part of lcs
            lcs += s1[i-1]
            
            # Got to diagonal cell
            i -= 1
            j -= 1
        
        # if chars are not matching then find larger of 2 cells and go one step in direction of larger one
        elif DP[i-1][j] > DP[i][j-1]:  # top cell value > left cell value 
            i -= 1  # go up
        else:  # left cell value > top cell value 
            
            j -= 1  # go down
            
    return print(lcs[::-1])
     
            
s1 = "ABCD"
s2 = "ACDF"


longest_common_subseq(s1, s2)

```

# Q3. Select the different pieces of the rod in such a way that resultant profit is maximum.

Ans: 

```python


def rod_cutting(pieces, Profit):
    
    DP = [[0]*(pieces+1) for _ in range(len(Profit))]
    
    # Construct the table
    for i in range(1, len(Profit)):  # starting_range=1 coz 0 is the base 
        for j in range(1, pieces+1):
            if i <= j:  # if piece value is less than the profit
                DP[i][j] = max(DP[i-1][j], Profit[i]+DP[i][j-i]) ## DP[i-1][j] : exluding current piece
            else:
                DP[i][j] = DP[i-1][j]
    
    i = len(Profit)-1
    j = pieces
    
    while i > 0 or j > 0:
        if DP[i][j] == DP[i-1][j]:  ## if current and top cells are matching then give item is not in solution.
            i -= 1  # Hence, descrese i for next iteration
        else: # if current and top cells are not matching then take this ; meaning current item is in solution.
            print("Take piece with length:", i, "meter")
            j -= i


# Example input
pieces = 5
Profit = [0, 2, 5, 7, 3, 9]

# Call the function
rod_cutting(pieces, Profit)

```
Output: 
 - Take piece with length: 2 meter
 - Take piece with length: 2 meter
 - Take piece with length: 1 meter

# Q4. 0/1 Knapsack Problem: you're given a set of items, each with a weight and a value, and your goal is to determine the combination of items to include in a knapsack of limited capacity such that the total value is maximized.

Ans:

```python

def knapsack_prob(N, M, W, V):
    
    DP = [[0 for _ in range(M+1)] for _ in range(N+1)]
    
    for i in range(1, N+1):
        for w in range(1, M+1):
            not_taking_item = DP[i-1][w]
            taking_item = 0
            
            if W[i] <= w:  #Check if current item's weight is less than knapsack's capacity
                taking_item = V[i] + DP[i-1][w-W[i]]  # value if taking current item
            
            DP[i][w] = max(not_taking_item, taking_item)
            
    print("Total benefit: %d" % DP[N][M])
    
    w = M
    for i in range(N, 0 , -1): #iterate through all items in DP table in backward direction
        #if current weight is not zero, and current and above cell values are not matching
        if DP[i][w] !=0 and DP[i][w] != DP[i-1][w]:
            
            print("We're taking item  #%d" % i)
            w = w-W[i]   # decrease the knapsack's capacity, since we've considered this item already
            
         
# Example input
num_of_items = 4
knapsack_capacity = 7
weights = [0, 1, 3, 4, 5]
profits = [0, 1, 4, 5, 7]

# Call the function
knapsack_prob(num_of_items, knapsack_capacity, weights, profits)

```
output:
- Total benefit: 9
  - We're taking item  #3
  - We're taking item  #2

# Q5. Find sum of first N Fibonacci number using Dynamic programming.
Ans: 

```python

# top-down approach
def fibonacci_memoization(n, DP):
    if n not in DP:
        DP[n] = fibonacci_memoization(n-1, DP) + fibonacci_memoization(n-2, DP)

    return DP[n]


# bottom-up approach
def fibonacci_tabulation(n, DP):

    for i in range(2, n+1):
        DP[i] = DP[i-1] + DP[i-2]

    return DP[n]

DP = {0: 1, 1: 1}


print("===== fibonacci_tabulation =====")
print(fibonacci_tabulation(4, DP))

# print("===== fibonacci_memoization =====")
# print(fibonacci_memoization(4, DP))

```

# Q1. Find the subset of numbers from a list which sum up to N.

Ans:

```python

def subset_sum(M, nums):
    
    DP = [[False for _ in range(M+1)] for _ in range(len(nums)+1)]
    
    #Initialize the first row and colum to be True
    for i in range(len(nums)+1):
        DP[i][0] = True
    
    #Construct the rest of the table
 
    for i in range(1, len(nums)+1):
        for j in range(1, M+1):
                
            if j < nums[i-1]:   # if local sum value is less than the previous item
                DP[i][j] = DP[i-1][j]  # Don't include the item
                
            else:  # if local sum value is not less than the previous item
                if DP[i-1][j]:  # If previous cell value is True
                    DP[i][j] = DP[i-1][j]
                else:
                    DP[i][j] = DP[i-1][j-nums[i-1]]

    # Get the subset values which sum upto the desired sum.
    j = M
    i = len(nums)
    while i > 0 or j > 0:

        if DP[i][j] == DP[i-1][j]:  # If current cell item is same as above cell item. 
            i = i-1
        else:
            print('item for the subset: %d' % nums[i - 1])
            j = j-nums[i-1]  # Decrement the column index by actual integer, and decrement the row index by 1.
            i = i-1
        
                
M = 12
nums = [1, 2, 4, 6]

subset_sum(M, nums)

```

# Q2. Find the longest common subsequence between two strings.
Ans:

```python
def longest_common_subseq(s1, s2):
    
    DP = [[0 for _ in range(len(s1)+1)] for _ in range(len(s2)+1)]

    for i in range(len(s1)):
        DP[i][0] = 0

    # Construct the table
    for i in range(1, len(s1)+1):
        for j in range(1, len(s2)+1):
            
            if s1[i-1] == s2[j-1]: # if chars are matching
                DP[i][j] = DP[i-1][j-1]+1
            else:  
                DP[i][j] = max(DP[i-1][j], DP[i][j-1])
                
    # Retrieve the longest common subsequence
    lcs = ''
    i, j = len(s1), len(s2)
    
    while i > 0 or j > 0:
        if s1[i-1] == s2[j-1]:  # if chars are matching then char is part of lcs
            lcs += s1[i-1]
            
            # Got to diagonal cell
            i -= 1
            j -= 1
        
        # if chars are not matching then find larger of 2 cells and go one step in direction of larger one
        elif DP[i-1][j] > DP[i][j-1]:  # top cell value > left cell value 
            i -= 1  # go up
        else:  # left cell value > top cell value 
            
            j -= 1  # go down
            
    return print(lcs[::-1])
     
            
s1 = "ABCD"
s2 = "ACDF"


longest_common_subseq(s1, s2)

```

# Q3. Select the different pieces of the rod in such a way that resultant profit is maximum.

Ans: 

```python


def rod_cutting(pieces, Profit):
    
    DP = [[0]*(pieces+1) for _ in range(len(Profit))]
    
    # Construct the table
    for i in range(1, len(Profit)):  # starting_range=1 coz 0 is the base 
        for j in range(1, pieces+1):
            if i <= j:  # if piece value is less than the profit
                DP[i][j] = max(DP[i-1][j], Profit[i]+DP[i][j-i]) ## DP[i-1][j] : exluding current piece
            else:
                DP[i][j] = DP[i-1][j]
    
    i = len(Profit)-1
    j = pieces
    
    while i > 0 or j > 0:
        if DP[i][j] == DP[i-1][j]:  ## if current and top cells are matching then give item is not in solution.
            i -= 1  # Hence, descrese i for next iteration
        else: # if current and top cells are not matching then take this ; meaning current item is in solution.
            print("Take piece with length:", i, "meter")
            j -= i


# Example input
pieces = 5
Profit = [0, 2, 5, 7, 3, 9]

# Call the function
rod_cutting(pieces, Profit)

```
Output: 
 - Take piece with length: 2 meter
 - Take piece with length: 2 meter
 - Take piece with length: 1 meter

# Q4. 0/1 Knapsack Problem: you're given a set of items, each with a weight and a value, and your goal is to determine the combination of items to include in a knapsack of limited capacity such that the total value is maximized.

Ans:

```python

def knapsack_prob(N, M, W, V):
    
    DP = [[0 for _ in range(M+1)] for _ in range(N+1)]
    
    for i in range(1, N+1):
        for w in range(1, M+1):
            not_taking_item = DP[i-1][w]
            taking_item = 0
            
            if W[i] <= w:  #Check if current item's weight is less than knapsack's capacity
                taking_item = V[i] + DP[i-1][w-W[i]]  # value if taking current item
            
            DP[i][w] = max(not_taking_item, taking_item)
            
    print("Total benefit: %d" % DP[N][M])
    
    w = M
    for i in range(N, 0 , -1): #iterate through all items in DP table in backward direction
        #if current weight is not zero, and current and above cell values are not matching
        if DP[i][w] !=0 and DP[i][w] != DP[i-1][w]:
            
            print("We're taking item  #%d" % i)
            w = w-W[i]   # decrease the knapsack's capacity, since we've considered this item already
            
         
# Example input
num_of_items = 4
knapsack_capacity = 7
weights = [0, 1, 3, 4, 5]
profits = [0, 1, 4, 5, 7]

# Call the function
knapsack_prob(num_of_items, knapsack_capacity, weights, profits)

```
output:
- Total benefit: 9
  - We're taking item  #3
  - We're taking item  #2

# Q5. Find sum of first N Fibonacci number using Dynamic programming.
Ans: 

```python

# top-down approach
def fibonacci_memoization(n, DP):
    if n not in DP:
        DP[n] = fibonacci_memoization(n-1, DP) + fibonacci_memoization(n-2, DP)

    return DP[n]


# bottom-up approach
def fibonacci_tabulation(n, DP):

    for i in range(2, n+1):
        DP[i] = DP[i-1] + DP[i-2]

    return DP[n]

DP = {0: 1, 1: 1}


print("===== fibonacci_tabulation =====")
print(fibonacci_tabulation(4, DP))

# print("===== fibonacci_memoization =====")
# print(fibonacci_memoization(4, DP))

```

# Q6. Search for occurrences of a pattern within a given text. The primary goal is to find all occurrences of a specified pattern in the text using  "Knuth–Morris–Pratt (KMP) algorithm.
Ans:

```python

def prepare_pi_table(pattern):
    pi_table = [0] * len(pattern)
    prefix_counter, i = 0, 1  # i: to iterate through elements of pattern

    while i < len(pattern):
        if pattern[i] == pattern[prefix_counter]:
            pi_table[i] = prefix_counter + 1
            i += 1
            prefix_counter += 1
        else:
            if prefix_counter != 0:
                prefix_counter = pi_table[prefix_counter - 1]
            else:
                pi_table[i] = 0
                i += 1

    return pi_table

def search_for_pattern(text, pattern):
    pi_table = prepare_pi_table(pattern)

    # i: to track elements in text, j: to track elements in pattern
    i, j = 0, 0

    while i < len(text) and j < len(pattern):
        if text[i] == pattern[j]:  # if chars in text and pattern match
            i += 1
            j += 1

            if j == len(pattern):  # means if pattern's length is covered then pattern found
                print('Pattern found at index %s' % (i - j))
                j = pi_table[j - 1]
        elif j != 0:
            j = pi_table[j - 1]
        else:
            i += 1

# Example usage
search_for_pattern('abababab', 'aba')

```

output:
 - Pattern found at index 0
 - Pattern found at index 2
 - Pattern found at index 4

# Q7.