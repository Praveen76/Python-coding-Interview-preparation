# Q1. Tower of Hanoi.

Ans: 
Hints: Objective: Transfer n disks from src to dest using middle disk
 - Step1. Transfer n-1 disks from src to middle using dest
 - Step2. Transfer n-1 disks from middle to dest using src.

```python

def hanoi_tower(disk, source, middle, destination):
    if disk == 0:
        print("Disk %s from %s to %s" % (disk, source, destination))
        return
    
    hanoi_tower(disk-1, source, destination, middle)
    print("Disk %s from %s to %s" % (disk, source, destination))
    hanoi_tower(disk-1, middle, source, destination)


hanoi_tower(2, 'A', 'B', 'C')

```

# Q2. Find sum of N Finbonacci numbers using head and tail recursion methods.
Ans:


Method 1: sum of N Fibonacci numbers using head recursion method.

```python
def fibonacci_head(n):
    if n == 0 or n == 1:
        return 1
    
    fib1 = fibonacci_head(n-1)
    fib2 = fibonacci_head(n-2)
    
    result = fib1 + fib2
    
    return result


print(fibonacci_head(5))

```

Method 2: sum of N Fibonacci numbers using tail recursion method.

```python
def fibonacci_tail(n, a=0, b=1):
    
    if n == 0:
        return a
    if n == 1:
        return b
 
    return fibonacci_tail(n-1, b, a+b)


fibonacci_tail(4, a=0, b=1)

```

# Q3. Find the factorial of a number.
Ans:

Method 1: Find the factorial of a number using the head recursion method.

```python

def factorial_head(n):
    if n == 0:
        return 1
    
    return n*factorial_head(n-1)
        
              
print(factorial_head(4))
```

Method 2: Find the factorial of a number using the tail recursion method.

```python
def factorial_tail(n, accumalator=1):
    if n == 1:
        return accumalator
    
    return factorial_tail(n-1, n * accumalator)
    
    
print(factorial_tail(4))

```

# Q3. Find the GCD( greatest common divisor) of two numbers. 
Ans:

```python

def gcd(a, b):
    
    # Base case: if b|a (without a remainder) then b is the GCD
    if a % b == 0:
        return b
     
    #Call function recursively 
    return gcd(b, a % b)


print(gcd(16, 4))

```


