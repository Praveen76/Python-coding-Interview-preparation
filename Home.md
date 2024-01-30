# Q1. How to check whether a string is palindrome or not?
Ans:

Sure thing! Here's a simple Python code to check if a given string is a palindrome:

```python
def is_palindrome(s):
    s = s.lower()  # Convert the string to lowercase for case-insensitive comparison
    s = ''.join(c for c in s if c.isalnum())  # Remove non-alphanumeric characters
    return s == s[::-1]

# Example usage:
word = "radar"
if is_palindrome(word):
    print(f"{word} is a palindrome!")
else:
    print(f"{word} is not a palindrome.")
```

This code defines a function `is_palindrome` that takes a string as input, converts it to lowercase, and removes non-alphanumeric characters. Then it checks if the modified string is equal to its reverse, indicating whether it's a palindrome or not. The example usage checks if the word "radar" is a palindrome. You can replace "radar" with any other string for testing.


**Method 2: **There are several ways to check for palindromes in Python. Here's another approach using a simple loop:

```python
def is_palindrome(s):
    s = s.lower()
    s = ''.join(c for c in s if c.isalnum())

    length = len(s)
    for i in range(length // 2):
        if s[i] != s[length - 1 - i]:
            return False
    return True

# Example usage:
word = "radar"
if is_palindrome(word):
    print(f"{word} is a palindrome!")
else:
    print(f"{word} is not a palindrome.")
```

In this code, the function `is_palindrome` iterates through the characters of the string from both ends towards the center, comparing each pair of characters. If it finds any pair that doesn't match, it returns `False`. If the loop completes without finding any non-matching pairs, it returns `True`.

Again, you can replace the value of the `word` variable with different strings to test for palindromes.

# Q3. Python code to print every 2nd character of the string?
Ans: 
Certainly! Here's a simple Python code snippet to print every 2nd character of a string:

```python
def print_every_second_character(s):
    result = s[1::2]
    print(result)

# Example usage:
my_string = "hello"
print_every_second_character(my_string)
```

In this code, the `print_every_second_character` function takes a string `s` as input and uses slicing to extract every 2nd character. The syntax `s[1::2]` means start from index 1 (the second character), and then take every 2nd character from there.

The example usage prints every 2nd character of the string "hello," so the output would be "el." You can replace the value of the `my_string` variable with different strings for testing.

**Method2**: Another way to print every 2nd character of a string in Python is to use a simple loop. Here's an example:

```python
def print_every_second_character(s):
    result = ""
    for i in range(1, len(s), 2):
        result += s[i]
    print(result)

# Example usage:
my_string = "hello"
print_every_second_character(my_string)
```

In this code, the function `print_every_second_character` iterates through the characters of the string using a loop with a step size of 2 (`range(1, len(s), 2)`). It then concatenates each 2nd character to the `result` string.

The example usage prints every 2nd character of the string "hello," resulting in the output "el." Feel free to replace the value of the `my_string` variable with different strings for testing.

# Q4. Merge the below lists to generate a list C, you should not use the sorted() function in python ?
          A = [1,2,3,5]
          B= [7,8,9,11,15]

Ans: Here are a few  methods to merge two sorted lists without using the `sorted()` function:

### Using `extend` and `sort`:
```python
A = [1, 2, 3, 5]
B = [7, 8, 9, 11, 15]

# Extend list A with elements of B
A.extend(B)

# Sort the merged list
A.sort()

# Result is in A
C = A
print("Merged List C:", C)
```

### Using `+=` and `sort`:
```python
A = [1, 2, 3, 5]
B = [7, 8, 9, 11, 15]

# Concatenate lists A and B and sort the result
C = A + B
C.sort()

print("Merged List C:", C)
```

### Using `heapq.merge` (requires Python 3.5+):
```python
import heapq

A = [1, 2, 3, 5]
B = [7, 8, 9, 11, 15]

# Use heapq.merge to merge sorted iterables
C = list(heapq.merge(A, B))

print("Merged List C:", C)
```

### Using a loop and `insert`:
```python
A = [1, 2, 3, 5]
B = [7, 8, 9, 11, 15]

# Initialize an empty list C
C = list(A)

# Iterate through elements in B and insert them in sorted order in C
for element in B:
    for i in range(len(C)):
        if element < C[i]:
            C.insert(i, element)
            break
    else:
        # If the element is greater than all elements in C, append it
        C.append(element)

print("Merged List C:", C)
```

These methods provide different approaches to achieve the same result. Choose the one that best fits your needs and preferences.

```python
A = [1, 2, 3, 5]
B = [7, 8, 9, 11, 15]

# Initialize an empty list C with the elements of A
C = list(A)

# Insert elements from B into C in sorted order
for element in B:
    inserted = False
    for i in range(len(C)):
        if element < C[i]:
            C.insert(i, element)
            inserted = True
            break

    if not inserted:
        # If the element is greater than all elements in C, append it
        C.append(element)

print("Merged List C:", C)

```
# Q4.1: Could an else clause exist without an if clause?
Ans:
In Python, the `for` loop can have an optional `else` clause. The `else` block is executed if the loop completes its iterations without encountering a `break` statement. In this specific case:

```python
for i in range(len(C)):
    if element < C[i]:
        C.insert(i, element)
        break
else:
    # If the loop completes without hitting the break statement, execute this block
    C.append(element)
```

This usage of the `else` clause with a `for` loop is a bit uncommon and might be confusing. It is used here to check if the inner loop completed without breaking. If it did, it means that the element being considered is greater than or equal to all elements in `C`, so it should be appended to the end of the list.

While this code works, it might be clearer to use a flag variable or a different approach to handle the logic more explicitly. For example:

```python
for element in B:
    inserted = False
    for i in range(len(C)):
        if element < C[i]:
            C.insert(i, element)
            inserted = True
            break
    if not inserted:
        C.append(element)
```

This way, the logic for appending the element if it's greater than all elements in `C` is more explicitly handled without relying on the `else` clause of the `for` loop.