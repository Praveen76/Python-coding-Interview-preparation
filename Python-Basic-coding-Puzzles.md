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
# Q4. How to extract common elements between two lists in python without using for loop?
Ans: 

**Method 1:**
You can use the `set` data type and its intersection method to find the common elements between two lists without using a for loop. Here's an example:

```python
list1 = [1, 2, 3, 4, 5]
list2 = [3, 4, 5, 6, 7]

common_elements = set(list1).intersection(list2)

print(list(common_elements))
```

In this example, `set(list1)` and `set(list2)` are used to convert the lists into sets, and then the `intersection` method is used to find the common elements. Finally, `list()` is used to convert the resulting set back into a list if needed.

**Method 2:**
You can use the `set` intersection operation to find the common elements between two lists without using a for loop. Here's an example:

```python
list1 = [1, 2, 3, 4, 5]
list2 = [3, 4, 5, 6, 7]

common_elements = list(set(list1) & set(list2))

print(common_elements)
```

In this example, `set(list1) & set(list2)` creates a set of common elements between `list1` and `list2`. Finally, we convert this set back to a list using `list()`.

Using sets for finding common elements is more efficient than using a loop, especially when dealing with large lists, as set operations have faster lookup times compared to iterating through lists.

Method 3:

```python
list1 = [1, 2, 3, 4, 5]
list2 = [3, 4, 5, 6, 7]

list3 =[]
for i in list1:
  if i in list2:
    list3.append(i)
print(list3)
```
# Q5. python code to sort dictionary by values?
Ans: 
Method 1:
Certainly! You can use the `sorted` function along with a lambda function to achieve this. Here's an example of how you can sort a dictionary by its values:

```python
my_dict = {'apple': 3, 'banana': 1, 'orange': 2, 'grape': 4}

# Sorting the dictionary by values
sorted_dict = dict(sorted(my_dict.items(), key=lambda item: item[1]))

print(sorted_dict)
```

In this example, `sorted` is used to sort the items of the dictionary based on their values. The `key` parameter specifies a function that is called to extract a comparison key from each item. In this case, a lambda function is used to extract the second element (the value) from each key-value pair. The result is a sorted list of tuples, which is then converted back to a dictionary using `dict()`.

There are several other ways to sort a dictionary by its values in Python. Here are a few alternative methods:

Method 2: Using `itemgetter` from the `operator` module:

```python
from operator import itemgetter

my_dict = {'apple': 3, 'banana': 1, 'orange': 2, 'grape': 4}

sorted_dict = dict(sorted(my_dict.items(), key=itemgetter(1)))

print(sorted_dict)
```

Method 3: Using a lambda function and the `items` method:

```python
my_dict = {'apple': 3, 'banana': 1, 'orange': 2, 'grape': 4}

sorted_dict = dict(sorted(my_dict.items(), key=lambda x: x[1]))

print(sorted_dict)
```
`key` is a parameter of the `sorted` function in Python. The `key` parameter allows you to specify a custom sorting criterion for the elements being sorted. It takes a function that is applied to each element before comparison during the sorting process.

Here's the basic syntax of the `sorted` function with the `key` parameter:

```python
sorted(iterable, key=key_function, reverse=False)
```

- `iterable`: The sequence to be sorted (e.g., a list, tuple, or dictionary).
- `key`: A function that takes an element from the `iterable` and returns a value for sorting.
- `reverse`: A Boolean flag indicating whether to sort in ascending (default) or descending order.

In the context of sorting a dictionary by values, the `key` parameter is commonly used with a lambda function to extract and use specific values for sorting.
Method 4: Using `collections.OrderedDict`:

```python
from collections import OrderedDict

my_dict = {'apple': 3, 'banana': 1, 'orange': 2, 'grape': 4}

sorted_dict = OrderedDict(sorted(my_dict.items(), key=lambda x: x[1]))

print(sorted_dict)
```

All of these methods will give you a dictionary sorted by values. Choose the one that you find most readable or suitable for your specific use case.

# Q 5.1: Where else can you use itemgetter?
Ans: `itemgetter` can be used in various scenarios where you need to access or manipulate elements in a sequence-like object such as a tuple, list, or dictionary. Here are some common use cases:

1. **Sorting by Multiple Keys:**
   You can use `itemgetter` to sort a list of tuples or other sequence-like objects based on multiple keys.

   ```python
   from operator import itemgetter

   data = [('apple', 3, 20), ('banana', 1, 15), ('orange', 2, 10), ('grape', 4, 25)]

   sorted_data = sorted(data, key=itemgetter(1, 2))  # Sort by the second and third elements
   ```

2. **Selecting Multiple Indices:**
   `itemgetter` can be used to select multiple indices from a sequence.

   ```python
   from operator import itemgetter

   data = (10, 20, 30, 40, 50)

   selected_elements = itemgetter(1, 3)(data)  # Select elements at indices 1 and 3
   ```

3. **Extracting Values from Dictionaries:**
   When dealing with dictionaries, `itemgetter` can be used to extract values associated with specific keys.

   ```python
   from operator import itemgetter

   my_dict = {'apple': 3, 'banana': 1, 'orange': 2}

   values = itemgetter('apple', 'orange')(my_dict)  # Extract values for 'apple' and 'orange'
   ```

4. **Accessing Nested Data Structures:**
   If you have nested data structures like lists of dictionaries, `itemgetter` can help extract values at specific depths.

   ```python
   from operator import itemgetter

   data = [{'name': 'John', 'age': 25}, {'name': 'Alice', 'age': 30}]

   names = itemgetter(0, 'name')(data)  # Extract the 'name' from the first dictionary
   ```

These are just a few examples, and `itemgetter` can be a handy tool whenever you need to access or manipulate elements in a sequence using indices or keys.

# Q 5.2: What is OrderedDict?
Ans: `OrderedDict` is a class in the `collections` module of the Python standard library. It is a dictionary subclass that maintains the order in which items were inserted into the dictionary. In a regular dictionary (`dict`), the order of items is not guaranteed to be preserved.

`OrderedDict` was introduced in Python 3.1, and it is useful when you need to iterate over the items in a dictionary in the order they were inserted. This can be particularly important in cases where the order of items matters, such as when you want to represent and maintain the order of configuration settings.

Here's a simple example to illustrate how `OrderedDict` works:

```python
from collections import OrderedDict

# Create an OrderedDict
ordered_dict = OrderedDict()

# Insert items in a specific order
ordered_dict['apple'] = 3
ordered_dict['banana'] = 1
ordered_dict['orange'] = 2
ordered_dict['grape'] = 4

# Iterate over the items in the order they were inserted
for key, value in ordered_dict.items():
    print(key, value)
```

The output will be:

```
apple 3
banana 1
orange 2
grape 4
```

As you can see, the items are printed in the order in which they were inserted into the `OrderedDict`. Using `OrderedDict` is not always necessary, but it can be beneficial when you need to maintain a specific order in your dictionary.

# Q6. Replace keys like "City" with city names such as "Newyork","London" in below code 

dctr= {
"Employees":[
                { "Name": "AB", "Dept_Code": 100, "City":"Newyork"},
                { "Name": "CD", "Dept_Code": 210, "City":"London"},
                { "Name": "EF", "Dept_Code": 300, "City":"Delhi"},
                { "ID": "PQ101","Dept_Code": 400, "City":"Chicago"},
                { "ID": "PQ102","Dept_Code": 500, "City":"Chicago"},
                { "ID": "REF10","Dept_Code": 750, "City":"London"},
                { "ID": "DEF50","Dept_Code": 601, "City":"London"}]
}

Ans:
You can achieve this by iterating through the dictionary and updating the "City" key to the respective city name. Here's the modified code:

```python
dctr = {
    "Employees": [
        {"Name": "AB", "Dept_Code": 100, "City": "Newyork"},
        {"Name": "CD", "Dept_Code": 210, "City": "London"},
        {"Name": "EF", "Dept_Code": 300, "City": "Delhi"},
        {"ID": "PQ101", "Dept_Code": 400, "City": "Chicago"},
        {"ID": "PQ102", "Dept_Code": 500, "City": "Chicago"},
        {"ID": "REF10", "Dept_Code": 750, "City": "London"},
        {"ID": "DEF50", "Dept_Code": 601, "City": "London"}
    ]
}

for employee in dctr["Employees"]:
    city_name = employee.pop("City")
    employee[city_name] = "City"

print(dctr)
```

This code iterates through each employee in the "Employees" list, pops the "City" key, and then adds a new key with the city name and the value "City". The resulting dictionary has the desired structure.

# Q7: Python code to get the items of List A not present in List B?
Ans:
```python
list_a = [1, 2, 3, 4, 5]
list_b = [3, 4, 5, 6, 7]

items_not_in_b = list(set(list_a) - set(list_b))

print(items_not_in_b)
```

# Q8: How to get the items not common to both Lists A and B?
Ans:
You can use set operations to get the items that are not common to both List A and List B. Specifically, you can use the symmetric difference operation (`^`). Here's an example:

```python
list_a = [1, 2, 3, 4, 5]
list_b = [3, 4, 5, 6, 7]

items_not_common = list(set(list_a) ^ set(list_b))

print(items_not_common)
```

In this example, `set(list_a) ^ set(list_b)` returns a set of items that are in either `list_a` or `list_b` but not in both. Finally, we convert this set back to a list using `list()`.

# Q9: 
