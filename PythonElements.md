# Python Elements Quick Reference

## Table of Contents
- [Variables and Data Types](#variables-and-data-types)
- [Operators](#operators)
- [Control Structures](#control-structures)
- [Lists and Arrays](#lists-and-arrays)
- [Functions](#functions)
- [String Operations](#string-operations)

## Variables and Data Types
```python
# Numeric Types
number = 42                    # Integer (no size limit)
decimal = 3.14                 # Float
complex_num = 1 + 2j          # Complex number

# Text Type
text = "Hello Python!"        # String (can use ' or ")
multiline = """
    Multiple
    lines
    of text
"""                          # Multi-line string

# Boolean Type
is_active = True             # Boolean (True or False)
is_empty = False

# Sequence Types
my_list = [1, 2, 3]         # List (mutable)
my_tuple = (1, 2, 3)        # Tuple (immutable)
my_range = range(5)         # Range (0 to 4)

# Mapping Type
my_dict = {                 # Dictionary
    "name": "Python",
    "version": 3.9
}

# Set Types
my_set = {1, 2, 3}         # Set (unique values)
frozen = frozenset([1,2,3]) # Immutable set

# None Type
empty_value = None         # Represents no value

# Type Checking
type(number)               # Check type
isinstance(number, int)    # Check if instance
```

## Operators
```python
# Arithmetic Operators
sum_result = 5 + 3        # Addition
diff = 10 - 4             # Subtraction
product = 4 * 2           # Multiplication
quotient = 15 / 3         # Division (float result)
floor_div = 15 // 3       # Floor division
remainder = 7 % 3         # Modulus
power = 2 ** 3           # Exponentiation

# Assignment Operators
number = 10
number += 5              # Add and assign
number -= 3              # Subtract and assign
number *= 2              # Multiply and assign
number /= 4              # Divide and assign
number //= 2             # Floor divide and assign
number **= 2             # Power and assign
number %= 3              # Modulus and assign

# Comparison Operators
is_equal = 5 == 5        # Equal to
not_equal = 5 != 3       # Not equal to
greater = 7 > 3          # Greater than
less = 4 < 8             # Less than
greater_eq = 5 >= 5      # Greater than or equal
less_eq = 4 <= 4         # Less than or equal

# Logical Operators
and_result = True and False  # Logical AND
or_result = True or False    # Logical OR
not_result = not True       # Logical NOT

# Identity Operators
is_same = [] is []          # Identity comparison
not_same = [] is not []     # Negative identity

# Membership Operators
in_list = 1 in [1, 2, 3]    # Check membership
not_in = 4 not in [1, 2, 3] # Check non-membership
```

## Control Structures
```python
# If-Elif-Else Statements
if score >= 90:
    print("A grade")
elif score >= 80:
    print("B grade")
else:
    print("Below B")

# Match Statement (Python 3.10+)
match day:
    case 1:
        print("Monday")
    case 2:
        print("Tuesday")
    case _:                  # Default case
        print("Other day")

# While Loop
i = 0
while i < 5:                # Loop with condition
    print(i)
    i += 1

# For Loop
for i in range(5):          # Loop through range
    print(i)

# For Loop with Collection
numbers = [1, 2, 3, 4, 5]
for num in numbers:         # Loop through collection
    print(num)

# Loop Control
for i in range(10):
    if i == 3:
        continue           # Skip current iteration
    if i == 8:
        break             # Exit loop
    print(i)

# Comprehensions
squares = [x**2 for x in range(5)]           # List comprehension
even_squares = [x**2 for x in range(5) if x % 2 == 0]  # With condition
```

## Lists and Arrays
```python
# List Creation
numbers = [1, 2, 3, 4, 5]   # List literal
mixed = [1, "two", 3.0]     # Mixed types
nested = [[1, 2], [3, 4]]   # Nested lists

# List Operations
numbers.append(6)           # Add element
numbers.extend([7, 8])     # Add multiple elements
numbers.insert(0, 0)       # Insert at position
numbers.remove(1)          # Remove value
popped = numbers.pop()     # Remove and return
numbers.sort()             # Sort in place
sorted_nums = sorted(numbers)  # Return sorted copy

# List Slicing
first_three = numbers[:3]   # First three elements
last_three = numbers[-3:]   # Last three elements
steps = numbers[::2]        # Every second element
reversed_list = numbers[::-1]  # Reverse list

# NumPy Arrays (if using NumPy)
import numpy as np
array = np.array([1, 2, 3])  # NumPy array
matrix = np.array([[1,2], [3,4]])  # 2D array
```

## Functions
```python
# Basic Function
def print_message():
    print("Hello!")

# Function with Parameters
def add(a, b):
    return a + b

# Default Parameters
def greet(name="World"):
    print(f"Hello, {name}!")

# Multiple Return Values
def get_coordinates():
    return 5, 10            # Returns tuple

# *args and **kwargs
def flexible_function(*args, **kwargs):
    print(f"Args: {args}")
    print(f"Kwargs: {kwargs}")

# Lambda Functions
square = lambda x: x**2     # Anonymous function

# Function Annotations
def process_data(text: str) -> str:
    return text.upper()

# Decorators
def my_decorator(func):
    def wrapper():
        print("Before")
        func()
        print("After")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")
```

## String Operations
```python
# String Creation
str1 = "Hello"              # Single or double quotes
str2 = 'Python'
multiline = """Multiple
line string"""              # Triple quotes

# String Methods
text = "Hello World"
length = len(text)          # String length
upper = text.upper()        # Convert to uppercase
lower = text.lower()        # Convert to lowercase
title = text.title()        # Title case
stripped = text.strip()     # Remove whitespace

# String Operations
first_char = text[0]        # Get character
substring = text[0:5]       # Get substring
reversed_str = text[::-1]   # Reverse string

# String Formatting
name = "Python"
# f-strings (Python 3.6+)
message = f"Hello, {name}!"
# format() method
message = "Hello, {}!".format(name)
# %-formatting
message = "Hello, %s!" % name

# String Methods
split_text = text.split()   # Split into list
joined = " ".join(["Hello", "World"])  # Join strings
replaced = text.replace("Hello", "Hi")  # Replace text
found = text.find("World")  # Find substring
count = text.count("l")     # Count occurrences
```
