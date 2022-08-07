# Welcome to the Python Cook Book ##############

- [Object Oriented Programing](oops/README.md)
- [Data Structure](data_structure/README.md)

# Object Oriented Programming ##############

Object-oriented programming is a programming paradigm in which
we are structuring programs so that properties and behaviors are bundled into individual objects.

*** Benefits ***  
Modularity for easier troubleshooting  
Reuse of code through inheritance  
Flexibility through polymorphism  
Effective problem solving  

---------------------------------------------
Inheritance
---------------------------------------------

Inheritance is the capability of one class to derive or inherit the properties from another class.    

*** Benefits ***  
It represents real-world relationships well.  
It provides reusability of a code. We don’t have to write the same code again and again.  
Also, it allows us to add more features to a class without modifying it.  

*** Types ***  
Single inheritance  
Multiple Inheritance  
Multilevel Inheritance  
Hierarchical : More than one derived classes are created from a single base  
Hybrid : Combination of multiple inheritance in single hierarchy  

What is object class?  
Like Java Object class, in Python (from version 3.x), object is root of all classes.  
```python
class Person(object):
    # Constructor
    def __init__(self, name):
        self.name = name

    def getName(self):
        return self.name

    def isEmployee(self):
        return False

# Inherited or Subclass (Note Person in bracket)
class Employee(Person):

    def isEmployee(self):
        return True

# Inherited or Subclass (Note Person in bracket)
class Manager(Employee, Person):
    # MRO : Method Resolution order is always override method of Employee (left most first)
    # If you are changing the order of the base class inheritance order then it will change
    # the execution of the methods if methods common in both class have same method

    def isEmployee(self):
        return True

emp = Person("Person1")  # An Object of Person
print(emp.getName(), emp.isEmployee()) # Person1 False
emp = Employee("Person2") # An Object of Employee
print(emp.getName(), emp.isEmployee()) # Person2 True

print(isinstance(emp, Person)) # True
print(issubclass(Employee, Person)) # True
print(issubclass(Person, object)) # True

```

---------------------------------------------
Polymorphism
---------------------------------------------

The word polymorphism means having many forms.  
polymorphism means the same function name (but different signatures) being used for different types.  

Method Overloading : Not possible in Python  
Operator Overloading  
Duck Typing  
Method Overriding  

Operator Overloading
---------------------
```python
10 + 2 = 12
"Hello"+"world" = "Hello world"

That means the same addition operator is differntly worked in the integer and string """
```

```python
class Students:

    def __init__(self, m1, m2):
        self.m1 = m1
        self.m2 = m2

    def __add__(self, other):
        m1 = self.m1 + other.m1
        m2 = self.m2 + other.m2
        m3 = Students(m1, m2)
        return m3

s1 = Students(10,20)
s2 = Students(30,40)
s3 = s1 + s2 # the definition of the plus is not changed (override) by the __add__ method
print(s3.m1, s3.m2) # 40 60
```

------------
Duck Typing
------------

Where the type or the class of an object is less important than the method it defines
Using Duck Typing, we do not check types at all. Instead, we check for the presence of a given method or attribute.
Duck-typing emphasis what the object can really do, rather than what the object is.

```python
class TextBox:
    def draw(self):
        print("Draw textbox")

class DropDown:
    def draw(self):
        print("Draw dropdown")

def draw(control):
    control.draw()

t = TextBox()
t.draw()
d = DropDown()
d.draw()
```

-----------------
Method Overriding
-----------------

```python
class Parent():
    # Constructor
    def __init__(self):
        self.value = "Inside Parent"
    # Parent's show method
    def show(self):
        print(self.value)
# Defining child class
class Child(Parent):
    # Constructor
    def __init__(self):
        self.value = "Inside Child"
    # Child's show method
    def show(self):
        # Parent.show(self)
        # super().show()
        print(self.value)
# Driver's code
obj1 = Parent()
obj2 = Child()
obj1.show() # Inside Parent
obj2.show() # Inside Child
```

---------------------------------------------
Abstraction
---------------------------------------------


Abstraction is defined as a process of handling complexity by hiding unnecessary information from the user
Abstraction provides a programmer to hide all the irrelevant data/process of an application in order
to reduce complexity and increase the efficiency of the program.  
BEST EXAMPLE : ORM (We don't know what happend behind the orm objects which deals with the Database)

```python
class Stream:

    def open(self):
        return ("Open")

class FileStream(Stream):

    def read(self):
        return ("Filestream is reading")

class NetworkStream(Stream):

    def read(self):
        return ("NetworkStream is reading")

# Stream is the common class so if we are calling
s = Stream()
s.open()
# Issue 1: that doesn't mean anything.. like which kind of streame is opening ?
# Issue 2: FileStream and NetworkStream has read method now in future if we have third stream like xyzStream
#          then that class have also a readLine or readStream method which performs the same method like read
#          so this is not consistent convensionally. There is no way to enforce common Interface to read different streams

# So for that we have a concept of ABS (Abstract base class)
# to manage the proper consistence convensional and common interface throughout with whole program.

from abc import ABC, abstractmethod

class Stream(ABC):
    def open(self):
        return ("Open")

    @abstractmethod
    def read(self):
        pass

class FileStream(Stream):
    def read(self):
        return ("Filestream is reading")

class NetworkStream(Stream):
    def read(self):
        return ("NetworkStream is reading")

class MemoryStream(Stream):
    pass

class Memory2Stream(Stream):
    def read(self):
        return ("Memory2Stream is reading")

# Stream is the common class so if we are calling
s = Stream()
s.read() # TypeError: Can't instantiate abstract class Stream with abstract methods read

s = MemoryStream()
# TypeError: Can't instantiate abstract class Stream with abstract methods read
# That means, you have to define read method in the class mandatory
s.read()

s = Memory2Stream()
print(s.read()) # Memory2Stream is reading

```

--------------------------------------------
Encapsulation
--------------------------------------------


It describes the idea of wrapping data and the methods that work on data within one unit.  
This puts restrictions on accessing variables and methods directly and can prevent the accidental modification of data.

```python
class Base:
    def __init__(self):
        self.a = "XYZ"
        self.__c = "XYZ"
class Derived(Base):
    def __init__(self):
        Base.__init__(self)
        print("Calling private member of base class: ")
        print(self.__c)

obj1 = Base()
print(obj1.a) # XYZ
print(obj1.__c) # AttributeError: 'Base' object has no attribute '__c'
```

# Data Structure

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

## Stacks : LIFO
```python
browsing_history = []
browsing_history.append(1)
browsing_history.append(2)
browsing_history.append(3)
browsing_history.pop()
browsing_history[-1]
```

## Queue : FIFO

```python
from collections import deque
queue = deque([])
queue.append(1)
queue.append(2)
queue.append(3)
print(queue)
queue.popleft()
print(queue)
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

## Static and Class Methods

Static methods, much like class methods, are methods that are bound to a class rather than its object.  

They do not require a class instance creation. So, they are not dependent on the state of the object.  

The difference between a static method and a class method is:  
  
Static method knows nothing about the class and just deals with the parameters.  
Class method works with the class since its parameter is always the class itself.  
They can be called both by the class and its object.  

```python
class Car:
    tyre = 5
    def run(self):
        print("Hrummmmm....")

    # class method is used with cls parameter like self and we can call using class name directly
    @classmethod
    def accelarate(cls):
        print(cls.tyre)

    """
        static method has no attribute like self and cls. when we use some kind of stuff which not requried
        any class or object instance then we are using static method. if you remove @staticmethod as decorator
        you will get error like getDetails() takes 0 positional arguments but 1 was given
    """
    @staticmethod
    def getDetails():
        print("This is good car")

c = Car()
print(Car.run(c))  # Hrummmmm....
Car.accelarate() # 5
c.accelarate() # 5
Car.getDetails() # This is good car
c.getDetails() # This is good car
```

## Private Members

```python
class Car:
    tyre = 5
    def __init__(self, tyre):
        self.__tyre = tyre
    def run(self):
        print("Hrummmmm....")

c = Car(10)
print(c.tyre) # 5
print(c.__tyre) # AttributeError: 'Car' object has no attribute '__tyre'
print(c.__dict__) # {'_Car__tyre': 10}
print(c._Car__tyre) # 10
```

## Properties

```python
# This is the simple example of getter and setter but this is not the original use of python here.
class Car:

    def __init__(self, price):
        self.set_price(price)

    def get_price(self):
        return self.__price

    def set_price(self, value):
        if value < 0:
            raise ValueError("No Negative Value")
        self.__price = value

c = Car(10)
c.get_price()

```

This is advance version to use property keyword here to get and set the value using
two function parameter pass to property keyword

```python
class Car:

    def __init__(self, price):
        self.set_price(price)

    def get_price(self):
        return self.__price

    def set_price(self, value):
        if value < 0:
            raise ValueError("No Negative Value")
        self.__price = value
    # Option 1
    price = property (get_price, set_price)

    # Option 2
    price = property()
    # assign fget
    price = price.getter(get_price)
    price = price.setter(set_price)

c = Car(10)
c.price = -1 # raise ValueError
c.price = 20 # set value to 20
print(c.price)

```

MOST ADVANCED

```python
class Car:

    @property
    def price(self):  # this should become the property value if you change the value to pricexyz
        return self.__price

    @price.setter
    def price(self, value):  # then you have to change to pricexyz here as well.
        if value < 0:
            raise ValueError("No Negative Value")
        self.__price = value


c = Car()
c.price = -1 # raise ValueError
c.price = 20 # set value to 20
print(c.price) # 20
print(c.pricexyz) # 20
# If you comment the setter method and then try to assign the value
c.price = 20 # rasie AttributeError : can't set attribute
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


# Data structure & Algorithms

---------------------------------------------
Binary Search
---------------------------------------------
```python
from util import time_it

@time_it
def linear_search(numbers_list, number_to_find):
    for index, element in enumerate(numbers_list):
        if element == number_to_find:
            return index
    return -1

@time_it
def binary_search(numbers_list, number_to_find):
    left_index = 0
    right_index = len(numbers_list) - 1
    mid_index = 0

    while left_index <= right_index:
        mid_index = (left_index + right_index) // 2
        mid_number = numbers_list[mid_index]

        if mid_number == number_to_find:
            return mid_index

        if mid_number < number_to_find:
            left_index = mid_index + 1
        else:
            right_index = mid_index - 1

    return -1

def binary_search_recursive(numbers_list, number_to_find, left_index, right_index):
    if right_index < left_index:
        return -1

    mid_index = (left_index + right_index) // 2
    if mid_index >= len(numbers_list) or mid_index < 0:
        return -1

    mid_number = numbers_list[mid_index]

    if mid_number == number_to_find:
        return mid_index

    if mid_number < number_to_find:
        left_index = mid_index + 1
    else:
        right_index = mid_index - 1

    return binary_search_recursive(numbers_list, number_to_find, left_index, right_index)

if __name__ == '__main__':
    numbers_list = [12, 15, 17, 19, 21, 24, 45, 67]
    number_to_find = 21

    index = binary_search_recursive(numbers_list, number_to_find, 0, len(numbers_list))
    print(f"Number found at index {index} using binary search")
```
---------------------------------------------
Bubble Sort
---------------------------------------------
```python
def bubble_sort(elements):
    size = len(elements)

    for i in range(size-1):
        for j in range(size-1):
            if elements[j] > elements[j+1]:
                elements[j], elements[j+1] = elements[j+1], elements[j]

if __name__ == '__main__':
    elements = [5,9,2,1,67,34,88,34]
    elements = ["mona", "dhaval", "aamir", "tina", "chang"]

    bubble_sort(elements)
    print(elements)
```


---------------------------------------------
Linked List
---------------------------------------------
```python
class Node:
    def __init__(self, data=None, next=None):
        self.data = data
        self.next = next

class LinkedList:
    def __init__(self):
        self.head = None

    def print(self):
        if self.head is None:
            print("Linked list is empty")
            return
        itr = self.head
        llstr = ''
        while itr:
            llstr += str(itr.data)+' --> ' if itr.next else str(itr.data)
            itr = itr.next
        print(llstr)

    def get_length(self):
        count = 0
        itr = self.head
        while itr:
            count+=1
            itr = itr.next

        return count

    def insert_at_begining(self, data):
        node = Node(data, self.head)
        self.head = node

    def insert_at_end(self, data):
        if self.head is None:
            self.head = Node(data, None)
            return

        itr = self.head

        while itr.next:
            itr = itr.next

        itr.next = Node(data, None)

    def insert_at(self, index, data):
        if index<0 or index>self.get_length():
            raise Exception("Invalid Index")

        if index==0:
            self.insert_at_begining(data)
            return

        count = 0
        itr = self.head
        while itr:
            if count == index - 1:
                node = Node(data, itr.next)
                itr.next = node
                break

            itr = itr.next
            count += 1

    def remove_at(self, index):
        if index<0 or index>=self.get_length():
            raise Exception("Invalid Index")

        if index==0:
            self.head = self.head.next
            return

        count = 0
        itr = self.head
        while itr:
            if count == index - 1:
                itr.next = itr.next.next
                break

            itr = itr.next
            count+=1

    def insert_values(self, data_list):
        self.head = None
        for data in data_list:
            self.insert_at_end(data)

    def get_middel_node(self, key):
        count = 0
        iter = self.head
        while iter:
            count += 1
            if count == key:
                return iter.data
            iter = iter.next


if __name__ == '__main__':
    ll = LinkedList()
    ll.insert_values(["banana","mango","grapes","orange"])
    ll.insert_at(1,"blueberry")
    ll.remove_at(2)
    ll.print()

    ll.insert_values([45,7,12,567,99])
    ll.insert_at_end(67)
    ll.get_middel_node(2) # mango
    ll.get_middel_node(4) # orange
    ll.print()
```

---------------------------------------------
Simple Tree
---------------------------------------------

```python
class TreeNode:
    def __init__(self, data):
        self.data = data
        self.children = []
        self.parent = None

    def get_level(self):
        level = 0
        p = self.parent
        while p:
            level += 1
            p = p.parent

        return level

    def print_tree(self):
        spaces = ' ' * self.get_level() * 3
        prefix = spaces + "|__" if self.parent else ""
        print(prefix + self.data)
        if self.children:
            for child in self.children:
                child.print_tree()

    def add_child(self, child):
        child.parent = self
        self.children.append(child)

def build_product_tree():
    root = TreeNode("Electronics")

    laptop = TreeNode("Laptop")
    laptop.add_child(TreeNode("Mac"))
    laptop.add_child(TreeNode("Surface"))
    laptop.add_child(TreeNode("Thinkpad"))

    cellphone = TreeNode("Cell Phone")
    cellphone.add_child(TreeNode("iPhone"))
    cellphone.add_child(TreeNode("Google Pixel"))
    cellphone.add_child(TreeNode("Vivo"))

    tv = TreeNode("TV")
    tv.add_child(TreeNode("Samsung"))
    tv.add_child(TreeNode("LG"))

    root.add_child(laptop)
    root.add_child(cellphone)
    root.add_child(tv)

    root.print_tree()

if __name__ == '__main__':
    build_product_tree()
```

---------------------------------------------
Binary Tree
---------------------------------------------
Every node has at most 2 child nodes.  

Binary Search Tree : left side nodes values less than root node.  
   Cannot have duplicate values  
   Every Iteration we reduce search space by 1/2.  
n = 8 , 8 > 4 > 2 > 1  
Total 3 Iteration so it means,  
log<sub>2</sub>8 = 3  

Traversal Techniques:  
Breadth first Search  
Depth first Search  
    -- In Order Traversal  
    -- Pre Order Traversal  
    -- Post Order Traversal  
![Binary tree](./img/binary_tree.png?raw=true "Binary tree")

# Problem Solving Programs

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
```