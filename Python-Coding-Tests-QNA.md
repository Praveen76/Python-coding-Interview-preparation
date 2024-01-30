# Q1. Spartacus has recently broken away from the Ludus and earned his freedom. But now he stands up front with a huge task. He is given a very large integer, and he needs to tell whether the integer is divisible by 11 or not. Write a program to help him solve this final problem that stands between him and Mira spending a happy life together.

Input Format: The only line of input contains an integer N
Constraints: The number of digits in the given integer will not exceed 106
Output Format: Print "Yes" if the divisibility holds, else print "No"

Evaluation Parameters:
  Sample Input = 121

# Complete the 'solution' function below.

The function is expected to return an STRING.
The function accepts STRING s as parameter.

```python
def solution(s):
	# Write your code here
```

```python
def solution(s):
    # Convert the string to a list of integers
    digits = [int(char) for char in s]

    # Calculate the alternating sum of digits
    digit_sum = sum((-1) ** i * digit for i, digit in enumerate(digits))

    # Check if the sum is divisible by 11
    if digit_sum % 11 == 0:
        return "Yes"
    else:
        return "No"


# Example usage:
input_number = input().strip()
result = solution(input_number)
print(result)
```
Output : Yes


# Q2: You are given a number n. You have to tell whether it is possible to express that number as a sum of two prime numbers as well as the sum of a prime and non-prime number separately. Return "Yes" if it is possible, or else return "No". (without quotes)

Note -: A number is said to be a prime number if it has only 2 positive factors which is 1 and the number itself.

Input Format: First-line of input contains an integer n.
Constraints: 1 ≤ n ≤ 105
Output Format: Return the string as required.

The function is expected to return an STRING.
The function accepts INTEGER n as parameter.

```python
def is_prime(num):
    if num < 2:
        return False
    for i in range(2, int(num**0.5) + 1):
        if num % i == 0:
            return False
    return True

def summingPrime(n):
    # Check if n can be expressed as the sum of two prime numbers
    for i in range(2, n):
        if is_prime(i) and is_prime(n - i):
            return "No"

    # Check if n can be expressed as the sum of a prime and non-prime number separately
    for i in range(2, n):
        if is_prime(i) and not is_prime(n - i):
            return "Yes"

    return "No"

# Example usage:
n = int(input())
result = summingPrime(n)
print(result)
```