# Q1: Write a while/for loop that sums the values 1 through end, inclusive. end is a variable that we define for you. So, for example, if we define end to be 6, your code should print out the result: 21. i.e. 1+2+3+4+5+6 = 21 .
Ans: 
Using While loop:
```python
end = 6  # You can change this value to any desired positive integer

# Initialize variables
sum_result = 0
current_value = 1

# While loop to sum values
while current_value <= end:
    sum_result += current_value
    current_value += 1

# Print the result
print(sum_result)
```

```python
end = 6  # You can change this value to any desired positive integer
# Initialize variables
sum_result = 0
current_value = 1

# for loop to sum values
for i in range(1, end+1):
       sum_result += i

# Print the result
print(sum_result)
```

# Q2: Write a program that prints the number of times the string 'bob' occurs in s. For example, if s = 'azcbobobegghakl', then your program should print Number of times bob occurs is: 2.

Ans: 
```python
s = 'azcbobobegghakl'  # You can change this string to any desired input

# Initialize a counter for occurrences
count_bob = 0

# Iterate through the string to find occurrences of 'bob'
for i in range(len(s) - 2):
    if s[i:i+3] == 'bob':
        count_bob += 1

# Print the result
print("Number of times bob occurs is:", count_bob)
```
- output : Number of times bob occurs is: 2

# Q3: Write a program that prints the longest substring of s in which the letters occur in alphabetical order. For example, if s = 'azcbobobegghakl', then your program should print Longest substring in alphabetical order is: beggh . In the case of ties, print the first substring. For example, if s = 'abcbcd', then your program should print Longest substring in alphabetical order is: abc
Ans:

```python
s = 'azcbobobegghakl'  # You can change this string to any desired input

# Initialize variables
current_substring = s[0]
longest_substring = s[0]

# Iterate through the string to find the longest alphabetical substring
for i in range(1, len(s)):
    if s[i] >= s[i-1]:
        current_substring += s[i]
    else:
        current_substring = s[i]

    # Update the longest substring if the current one is longer
    if len(current_substring) > len(longest_substring):
        longest_substring = current_substring

# Print the result
print("Longest substring in alphabetical order is:", longest_substring)
```
- Output: Longest substring in alphabetical order is: beggh
