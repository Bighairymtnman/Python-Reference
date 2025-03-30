# Python Advanced Concepts

## Table of Contents
- [Decorators](#decorators)
- [Generators and Iterators](#generators-and-iterators)
- [Context Managers](#context-managers)
- [Metaclasses](#metaclasses)
- [Concurrency](#concurrency)
- [Advanced Collections](#advanced-collections)

## Decorators
```python
# Function Decorator
def timer(func):
    from time import time
    def wrapper(*args, **kwargs):
        start = time()
        result = func(*args, **kwargs)
        print(f"Time taken: {time() - start:.2f}s")
        return result
    return wrapper

@timer
def slow_function():
    # Function will be timed
    pass

# Class Decorator
def singleton(cls):
    instances = {}
    def get_instance(*args, **kwargs):
        if cls not in instances:
            instances[cls] = cls(*args, **kwargs)
        return instances[cls]
    return get_instance

@singleton
class Database:
    # Only one instance will ever exist
    pass

# Decorator with Arguments
def repeat(times):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(times):
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator

@repeat(times=3)
def greet(name):
    print(f"Hello {name}")
```

## Generators and Iterators
```python
# Generator Function
def fibonacci(n):
    a, b = 0, 1
    for _ in range(n):
        yield a           # Yields next value
        a, b = b, a + b

# Generator Expression
squares = (x**2 for x in range(10))  # Memory efficient

# Custom Iterator
class CountDown:
    def __init__(self, start):
        self.start = start

    def __iter__(self):
        return self

    def __next__(self):
        if self.start <= 0:
            raise StopIteration
        self.start -= 1
        return self.start + 1

# Infinite Generator
def infinite_sequence():
    num = 0
    while True:
        yield num
        num += 1

# Generator Pipeline
def read_data():
    for i in range(100):
        yield i

def filter_even(numbers):
    for num in numbers:
        if num % 2 == 0:
            yield num

def multiply_by_two(numbers):
    for num in numbers:
        yield num * 2

# Using the pipeline
pipeline = multiply_by_two(filter_even(read_data()))
```

## Context Managers
```python
# Context Manager Class
class FileManager:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode
        self.file = None

    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file

    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.file:
            self.file.close()
        return False  # Don't suppress exceptions

# Using contextlib
from contextlib import contextmanager

@contextmanager
def timer():
    from time import time
    start = time()
    yield                  # User code runs here
    print(f"Elapsed: {time() - start:.2f}s")

# Nested Context Managers
with FileManager('file1.txt', 'r') as f1, \
     FileManager('file2.txt', 'w') as f2:
    content = f1.read()
    f2.write(content.upper())

# Async Context Manager
class AsyncResource:
    async def __aenter__(self):
        await self.open()
        return self

    async def __aexit__(self, exc_type, exc, tb):
        await self.close()
```

## Metaclasses
```python
# Basic Metaclass
class LoggedMeta(type):
    def __new__(cls, name, bases, attrs):
        # Add logging to all methods
        for key, value in attrs.items():
            if callable(value):
                attrs[key] = cls.log_call(value)
        return super().__new__(cls, name, bases, attrs)

    @staticmethod
    def log_call(func):
        def wrapper(*args, **kwargs):
            print(f"Calling {func.__name__}")
            return func(*args, **kwargs)
        return wrapper

# Using Metaclass
class MyClass(metaclass=LoggedMeta):
    def my_method(self):
        pass

# Abstract Base Class with Metaclass
from abc import ABCMeta, abstractmethod

class Interface(metaclass=ABCMeta):
    @abstractmethod
    def my_abstract_method(self):
        pass

# Metaclass for Singleton
class Singleton(type):
    _instances = {}
    
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]
```

## Concurrency
```python
# Threading
import threading

def worker(num):
    print(f'Worker {num}')

threads = []
for i in range(5):
    t = threading.Thread(target=worker, args=(i,))
    threads.append(t)
    t.start()

# Asyncio
import asyncio

async def fetch_data():
    await asyncio.sleep(1)  # Simulate IO
    return {'data': 'result'}

async def main():
    tasks = [fetch_data() for _ in range(3)]
    results = await asyncio.gather(*tasks)

# Multiprocessing
from multiprocessing import Process, Pool

def cpu_bound(n):
    return sum(i * i for i in range(n))

# Process Pool
with Pool() as pool:
    results = pool.map(cpu_bound, [1000000] * 3)

# Async Context Manager
async with aiohttp.ClientSession() as session:
    async with session.get('http://example.com') as response:
        data = await response.text()
```

## Advanced Collections
```python
from collections import (
    defaultdict, Counter, deque, 
    namedtuple, ChainMap
)

# DefaultDict
word_count = defaultdict(int)    # Default value of 0
for word in ['apple', 'banana', 'apple']:
    word_count[word] += 1

# Counter
inventory = Counter(['apple', 'banana', 'apple'])
inventory.most_common(1)         # Most common item
inventory.update(['apple'])      # Add items

# Deque (Double-ended queue)
history = deque(maxlen=5)        # Fixed-size queue
history.append('command1')
history.appendleft('command0')
history.pop()                    # Remove from right
history.popleft()               # Remove from left

# NamedTuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(11, y=22)
x, y = p                       # Unpacking

# ChainMap
defaults = {'color': 'red', 'size': 'medium'}
user_prefs = {'color': 'blue'}
settings = ChainMap(user_prefs, defaults)

# Custom Dict with Default
class AutoKeyDict(dict):
    def __missing__(self, key):
        self[key] = key
        return key

# Frozen Set
immutable = frozenset([1, 2, 3])

# Advanced Dict Operations
merged = {**dict1, **dict2}    # Merge dicts (Python 3.5+)
filtered = {k: v for k, v in d.items() if v > 0}  # Dict comp
```
