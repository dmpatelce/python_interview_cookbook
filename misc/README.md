
# Miscellaneous ##############

## Exmple 1

```python
Zeros = [0] * 5
# Output : [0,0,0,0,0] 
```

## Exmple 2
```python
letters = list(range(20))
A, B, *othres = letters
print(A,B,*othres)
# Output: 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19
```

## Enumerate

when dealing with iterators, we also get need to keep a count of iterations.  
Enumerate() method adds a counter to an iterable and returns it in a form of enumerating object.  
This enumerated object can then be used directly for loops or converted into a list of tuples using the list() method.  
enumerate(iterable, start=0) ... srart is the parameter from where the counting number starts

```python
letters = ["a", "b", "c"]
print(list(enumerate(letters))) # [(0, 'a'), (1, 'b'), (2, 'c')]
# Enumerate is iterable and generate key, value pair
for index, letter in enumerate(letters):
	print(index, letter) # 0 "a"    1 "b"    2 "c"
```

## Built in Functions
```python
id() # Returns the id of an object
dir() # Returns a list of the specified object's properties and methods
isinstance() # Returns True if a specified object is an instance of a specified object
iter() # Returns an iterator object
next() # Returns the next item in an iterable
bool() # Returns the boolean value of the specified object
dict() # Returns a dictionary (Array)
list() # Returns a list
int() # Returns an integer number
str() # Returns a string object
set() # Returns a new set object
print() # Prints to the standard output device
input() # Allowing user input
getattr() # Returns the value of the specified attribute (property or method)
hasattr() # Returns True if the specified object has the specified attribute (property/method)
setattr() # Sets an attribute (property/method) of an object
type() # Returns the type of an object
len() # Returns the length of an object
pow() # Returns the value of x to the power of y
max() # Returns the largest item in an iterable
min() # Returns the smallest item in an iterable
sum() # Returns a string object
abs()  # Returns the absolute value of a number
zip() # Returns an iterator, from two or more iterators
```

## String Methods

```python
str = "Hello World"
str.count() # Returns the number of times a specified value occurs in a string
str.startswith("H") # Returns true if the string starts with the specified value
str.endswith("d") # Returns true if the string ends with the specified value
str.capitalize() # Converts the first character to upper case
str.upper() # Converts a string into upper case
str.lower() # Converts a string into lower case
str.find("w") # Output : 7 Searches the string for a specified value and returns the position of where it was found
str.format() # Formats specified values in a string
str.index(3) # Searches the string for a specified value and returns the position of where it was found
str.islower # Returns true if all character is lower
str.isupper # Returns true if all character is upper
"#".join(str) # takes all items in an iterable and joins them into one string
str.replace("w", "$") # Returns a string where a specified value is replaced with a specified value
str.strip() # Returns a trimmed version of the string
str.rstrip() # Returns a right trim version of the string
str.lstrip() # Returns a left trim version of the string
```

## Exmple 4 : List

```python
letters = ["a", "b", "c"]
letters.append("d")
letters.index("a") # 0
letters.insert(0, "-")
letters.extend([1,2,3]) # concatenation of the list
letters.pop(0) # Remove first index value
letters.pop(1) # Remove specific index value
letters.pop(-1) # Remove last element
letters.remove("b") # Remove specific element if you don't know index and remove first occurance of "b"
del letters[0]
del letters[0:3]
letters.count("b") # list all the occurance of the b in the list even it is works with the string as well
letters.clear() # Clear all the elements of list
letters.copy() # Copy new list
letters.sort() # sort in asc
letters.sort(reverse=True) # sort in desc
letters.reverse() # sort in desc
sorted(letters) # it will return new list
sorted(letters, reverse=True) # it will return new list in desc order
```

## Dictionary Methods

```python
d = {"1": "xyz", "2": "345"}
d.clear() # Removes all the elements from the dictionary
d.copy() # Returns a copy of the dictionary
d.get() # Returns the value of the specified key
d.items() # Returns a list containing a tuple for each key value pair
d.keys() # Returns a list containing the dictionary's keys
d.pop() # Removes the element with the specified key
d.popitem() # Removes the last inserted key-value pair
d.update() # Updates the dictionary with the specified key-value pairs
d.values() # Returns a list of all the values in the dictionary
```

## Tuple Methods

```python
letters = ["a", "b", "c"]
letters.count() # Returns the number of times a specified value occurs in a tuple
letters.index() # Searches the tuple for a specified value and returns the position of where it was found
```

## File Methods

```python
f = open("demofile.txt", "r")
f.close() # Closes the file
f.read() # Returns the file content
f.readline() # Returns one line from the file
f.write() # Writes the specified string to the file
f.writelines() # Writes a list of strings to the file
f.flush() # flush internal buffer
```

## Lambda, Map, Reduce and Filter function
```python
items = [
    ("product1", 10),
    ("product2", 9),
    ("product3", 11),
]

def sort_item(item):
    return item[1]

items.sort(key=sort_item)
print(items)
```

## Lambda Function
```python
# A lambda function is a small anonymous function. A lambda function can take any number of arguments, but can only have one expression.
# lambda parameter : expression ... expression will return the value default
items.sort(key = lambda item: item[1])
print(items)
```

```python
# The power of lambda is better shown when you use them as an anonymous function inside another function.
def myfunc(n):
  return lambda a : a * n

mydoubler = myfunc(2)
mytripler = myfunc(3)

print(mydoubler(11))
print(mytripler(11))
```

## Map Function

```python
# map() function returns a map object(which is an iterator) of the results after applying the given function to each item of a given iterable (list, tuple etc.)
prices = list(map(lambda item: item[1], items)) # [10, 9, 11]
prices = [item[1] for item in items] # [10, 9, 11] ... List comprehension
```

```python
def addition(n):
    return n[1] + n[1]
result = map(addition, items)
print(list(result)) # [20, 18, 22]
result = map(lambda x: x[1] + x[1], items)

# List of strings
l = ['sat', 'bat', 'cat', 'mat']
# map() can listify the list of strings individually
test = list(map(list, l))
print(test) # [['s', 'a', 't'], ['b', 'a', 't'], ['c', 'a', 't'], ['m', 'a', 't']]
```

## Filter

```python
# filter
print(list(filter(lambda item: item[1] > 9, items)))
prices = [item[1] for item in items if item[1] > 9]  # [10, 11] ... List comprehension
```

## Reduce / Accumulate Function

```python
import itertools
import functools
lis = [1, 3, 4, 10, 4]
# printing summation using accumulate()
print("The summation of list using accumulate is :", end="")
print(list(itertools.accumulate(lis, lambda x, y: x+y)))
# The summation of list using accumulate is :[1, 4, 8, 18, 22]

# printing summation using reduce()
print("The summation of list using reduce is :", end="")
print(functools.reduce(lambda x, y: x+y, lis))
# The summation of list using reduce is :22
```

## Zip function

```python
a = [1,2,3]
b = [4,5,6]

print(zip(a, b))
cc = zip(a, b)
print(list(type(cc))) # [(1, 4), (2, 5), (3, 6)]
```

## Set
```python
# There is no index in Set like List
numbers = [1,1,2,3,4,4]
uniques = set(numbers)
uniques.add(5) # {1, 2, 3, 4, 5}
uniques.remove(3) # {1, 2, 4, 5}
len(uniques) # 4

first = set(numbers)
second = {1,5}

print(first | second) # {1, 2, 3, 4, 5} Union
print(first & second) # {1} Intersection
print(first - second) # {2, 3, 4} Difference
print(first ^ second) # {2, 3, 4, 5} Symatric difference
```

## Dictionary

```python
point = {"x": 1, "y": 2}
point = dict(x=1, y=2)
point["x"] = 10
point["z"] = 30
print(point["x"])
print(point.get("x"))
print(point.get("a", 0))
print(point)
del(point("x"))
point.items() # iterable
```

## Unpacking Operators

```python
numbers = [1,2,3]
print(numbers) # [1,2,3]
print(*numbers) # 1 2 3.. similar in javascript [...numbers]
print(1,2,3) # 1 2 3

values = list(range(5)) # [1,2,3,4,5]
values = [*range(5)] # [1,2,3,4,5] .... for positional arguments we have single *

first = {"x": 1}
second = {"y": 2}
combined = {**first, **second}
print(combined) # {"x": 1, "y": 2} .... for keyword arguments we have double **
```

## Contextual Function

```python
class Context:
    pass

def f1(context):
    a = context.a
    print("a:", a)

def f2(context):
    b = context.b
    print("b:", b)

c = Context()
c.a = 1
c.b = 2

f1(c) # a: 1
f2(c) # b: 2
```

## Iterators

Iterators are objects that can be iterated upon. An object which will return data, one element at a time
 Generally we can say, iterator has "__iter__" and "__next__" methods inbuilt.. example.. list, tuple, str etc

```python
# define a list
my_list = [4, 7, 0, 3]
my_iter = iter(my_list)
print(next(my_iter)) # 4
print(next(my_iter)) # 7
print(my_iter.__next__()) # 0
print(my_iter.__next__()) # 3
next(my_iter) # This will raise error, no items left (StopIteration)
```

custom Iterator

```python
class PowTwo:
    def __init__(self, max=0):
        self.max = max
    def __iter__(self):
        self.n = 0
        return self
    def __next__(self):
        if self.n <= self.max:
            result = 2 ** self.n
            self.n += 1
            return result
        else:
            raise StopIteration
# create an object
numbers = PowTwo(3)
# create an iterable from the object
i = iter(numbers)
# Using next to get to the next iterator element
print(next(i)) # 1
print(next(i)) # 2
print(next(i)) # 4
print(next(i)) # 8
print(next(i)) # StopIteration : Error
```

## Generators

Well, generator is used to rescue from the limitations of the Iterators.
Python generators are a simple way of creating iterators but in more efficient way
Let's say, we have a list, tuple, str as an iterator but what if we have millions of data ?
then this iterators consumes more memories at a time. So to overcome this issue we have a generator with yielding mechanism

The difference between return and yield is that while a return statement terminates a function entirely,
yield statement pauses the function saving all its states and later continues from there on successive calls.

Generator used to reduce the size of the bytes in memory

###### Exmaple 1:

```python
from sys import getsizeof

# with () it will generate list as a generator
# generator expressions are surrounded by parenthesis ()

values = (x*2 for x in range(10000))
print(getsizeof(values)) # 120 bytes.. even for millions of data the output should remain same
values = [x*2 for x in range(10000)]
print(getsizeof(values)) # 85647
```

###### Exmaple 2:

```python
def my_gen():
    n = 1
    yield n
    n += 1
    yield n
    n += 1
    yield n

a = my_gen()
next(a) # 1
next(a) # 2
next(a) # 3
next(a) # Traceback : StopIteration

# Using for loop
for item in my_gen():
    print(item)
```
###### Exmaple 3:

```python
# A simple generator for Fibonacci Numbers
def fib(limit):
    # Initialize first two Fibonacci Numbers
    a, b = 0, 1
    # One by one yield next Fibonacci Number
    while a < limit:
        yield a
        a, b = b, a + b
# Create a generator object
x = fib(5)
# Iterating over the generator object using next
print(x.next()) # In Python 3, __next__()
print(x.next())
print(x.next())
print(x.next())
print(x.next())
# Iterating over the generator object using for
# in loop.
print("\nUsing for in loop")
for i in fib(5):
    print(i)
```

## Closures


Closures can avoid the use of global values and provides some form of data hiding.
It can also provide an object oriented solution to the problem.

###### Example : 1

```python
def print_msg(msg):
    def printer():
        print(msg)
    return printer  # returns the nested function

another = print_msg("Hello")
another() # Output: Hello
```

###### Example : 2
```python
def make_multiplier_of(n):
    def multiplier(x):
        return x * n
    return multiplier

times3 = make_multiplier_of(3)
times5 = make_multiplier_of(5)

print(times3(9)) # Output: 27
print(times5(3)) # Output: 15
print(times5(times3(2))) # Output: 30
```

## Decorators

A decorator takes in a function, adds some functionality and returns it
This is also called metaprogramming because a part of the program tries to modify 
another part of the program at compile time.

```python
def make_pretty(func):
    def inner():
        print("I got decorated")
        func()
    return inner

def ordinary():
    print("I am ordinary")

ordinary()
pretty = make_pretty(ordinary)
pretty()
# Output
# I got decorated
# I am ordinary

# Conversion of the above methodology with Generators
@make_pretty
def ordinary():
    print("I am ordinary")

ordinary()
# Output
# I got decorated
# I am ordinary
```

```python
def smart_divide(func):
    def inner(a, b):
        if b == 0:
            print("Whoops! cannot divide")
            return

        return func(a, b)
    return inner

@smart_divide
def divide(a, b):
    print(a/b)

divide(2,5) # 0.4
divide(2,0) # Whoops! cannot divide
```

### Class Decorator

```python
class MyDecorator:
    def __init__(self, function):
        self.function = function
     
    def __call__(self):
 
        # We can add some code
        # before function call
        self.function()
        # We can also add some code
        # after function call.
 
# adding class decorator to the function
@MyDecorator
def function():
    print("Print Here")
 
function()
```

## Regular Expression

A Regular Expression (RegEx) is a sequence of characters that defines a search pattern.
Ref : https://www.programiz.com/python-programming/regex

```python
import re
pattern = '^a...s$'
test_string = 'abyss'
result = re.match(pattern, test_string) # True or False
result = re.findall(pattern, test_string) # return all matches

if result:
  print("Search successful.")
else:
  print("Search unsuccessful.")
```

## Partial Functions
partial function is a cool tool to write reusable code.  
Partial functions allow us to fix a certain number of arguments of a function and generate a new function.  
You can think of a partial function as an extension of another specified function. A partial function has the same functionality of the specified function, but with pre-filled values for a certain number of arguments.  

```python
from functools import *
  
# A normal function
def add(a, b):
    return a + b
  
# A partial function with b = 1 and c = 2
add_part = partial(add, 1, 2)
  
# Calling partial function
print(add_part()) # Output : 3
```

## Cipher
This is the encryption algorithm.

```python
def cipher(strr, count):
    cipher_arr = []
    for i in strr:
        # ord() will convert into the ascii value
        final = ord(i) + count
        if final > 122:
            final = 96 + (final - 122)
        # chr() convert ascii to character
        cipher_arr.append(chr(final))
    return "".join(cipher_arr)

print(cipher("abcxyz", 4))
