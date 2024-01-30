# Q1. Reverse a given list/array without creating another list/array.
Ans: To reverse a given list or array without creating another list or array (in-place reversal), you can use the following Python code:

```python
def reverse_in_place(arr):
    start_index = 0
    end_index = len(arr) - 1

    while start_index < end_index:
        # Swap elements at start_index and end_index
        arr[start_index], arr[end_index] = arr[end_index], arr[start_index]

        # Move indices towards the center
        start_index += 1
        end_index -= 1

# Example usage:
my_list = [1, 2, 3, 4, 5]
reverse_in_place(my_list)
print("Reversed List:", my_list)
```

This code defines a function `reverse_in_place` that takes a list as an argument and reverses it in-place using a two-pointer approach. The `start_index` starts from the beginning of the list, and the `end_index` starts from the end of the list. Elements at these indices are swapped, and the indices move towards the center until they meet.

Keep in mind that this modifies the original list, and if you want to preserve the original list, you may need to create a copy before applying the in-place reversal.

# Q2. Check whether given data is palindrome or not.
Ans:  

```python
# it has O(s) so basically linear running time complexity as far as the number
# of letters in the string is concerned
def is_palindrome(s):

    original_string = s
    # this is what we have implemented in the previous lecture in O(N)
    reversed_string = reverse(s)

    if original_string == reversed_string:
        return True

    return False


# O(N) linear running time where N is the number of letters in string s N=len(s)
def reverse(data):

    # string into a list of characters
    data = list(data)

    # pointing to the first item
    start_index = 0
    # index pointing to the last item
    end_index = len(data)-1

    while end_index > start_index:
        # keep swapping the items

        data[start_index], data[end_index] = data[end_index], data[start_index]
        start_index = start_index + 1
        end_index = end_index - 1

    # transform the list of letters into a string
    return ''.join(data)


if __name__ == '__main__':
    print(is_palindrome('Kevin'))
```

# Q3. Reverse a given integer.
Ans:

Method 1:
```python
def reverse_integer(n):

    reversed_integer = 0

    while n > 0:
        remainder = n % 10
        reversed_integer = reversed_integer*10 + remainder
        n = n // 10

    return reversed_integer


print(reverse_integer(12345678))

```

Method 2:
```python
my_list = '12345678'

def reverse_data(my_list):
    my_list = [char for char in my_list]
    
    i = 0
    j = len(my_list)-1

    while i < j:
        my_list[i], my_list[j] = my_list[j], my_list[i]
        i += 1
        j -= 1

    my_list = ''.join(char for char in my_list)
    return my_list

reverse_data(my_list)
```

# Q4. Construct an algorithm to check whether two words (or phrases) are anagrams or not!
Ans:

Method 1:
```python
def is_anagram(str1, str2):

    # if the length of the strings differ - they are not anagrams
    if len(str1) != len(str2):
        return False

    # we have to sort the letters of the strings and then we haev to compare
    # the letters with the same indexes
    # this is the bottlenect because it has O(NlogN)
    str1 = sorted(str1)
    str2 = sorted(str2)

    # after that we have to check the letters with the same indexes
    # O(N) running time
    for i in range(len(str1)):
        if str1[i] != str2[i]:
            return False

    # overall running time is O(NlogN)+O(N)=O(NlogN)

    return True



s1 = ['f', 'l', 'u', 's', 't', 'e', 'r']
s2 = ['r', 'e', 's', 't', 'f', 'e', 'l']

print(is_anagram(s1, s2))

```

Method 2: 
```python

s1 = 'silent'
s2 = 'listen'

if sorted(s1) == sorted(s2):
    print("True")
```