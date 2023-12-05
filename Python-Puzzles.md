# Q1. Python code to calculate the occurrence of each character in a string?
Ans:
Method 1:

You can use the `Counter` class from the `collections` module to easily calculate the occurrence of each character in a string. Here's an example:

```python
from collections import Counter

def count_characters(input_string):
    # Using Counter to count occurrences of each character
    char_count = Counter(input_string)

    # Printing the results
    for char, count in char_count.items():
        print(f"Character: {char}, Count: {count}")

# Example usage
input_string = "hello world"
count_characters(input_string)
```


Method 2: Without Counter function.

```python
# Function to calculate character occurrences in a string
def count_characters(input_string):
    # Create an empty dictionary to store character occurrences
    char_count = {}

    # Iterate through each character in the input string
    for char in input_string:
        # Check if the character is already in the dictionary
        if char in char_count:
            # If yes, increment the count
            char_count[char] += 1
        else:
            # If no, add the character to the dictionary with count 1
            char_count[char] = 1

    # Print the result
    for char, count in char_count.items():
        print(f"Character '{char}' occurs {count} time(s) in the string.")

# Example usage
input_string = "hello world"
count_characters(input_string)
```
# Q2. Python code to print every 2nd character of a string?
Ans:
Method1: You can achieve this in Python using string slicing. Here's an example code:

```python
def print_every_second_letter(input_string):
    result = input_string[1::2]
    print(result)

# Example usage:
input_string = "Hello, World!"
print_every_second_letter(input_string)
```

Method2: Another method to achieve the same result is by using a simple for loop. Here's an example:

```python
def print_every_second_letter(input_string):
    result = ""
    for i in range(1, len(input_string), 2):
        result += input_string[i]
    print(result)

# Example usage:
input_string = "Hello, World!"
print_every_second_letter(input_string)
```

In this example, the `for` loop iterates over the indices of the string, starting from 1 (the second letter) with a step size of 2, and appends each second letter to the `result` string. The final result is then printed.

# Q3. Python code to create a new list where each element at index i in list B is the product of all elements in list A except the element at index i in list A.
Ans: 

```python
def create_product_list_except_index(A):
    B = []  # Initialize the result list

    # Iterate over the indices of list A
    for i in range(len(A)):
        product = 1  # Initialize the product to 1

        # Iterate over the indices of list A again
        for j in range(len(A)):
            if i != j:  # Skip the element at the current index
                product *= A[j]  # Multiply the product by the element at index j

        B.append(product)  # Append the final product to list B

    return B  # Return the result list B

# Example usage:
A = [1, 2, 3, 4, 5]
B = create_product_list_except_index(A)
print("List A:", A)
print("List B:", B)
```
