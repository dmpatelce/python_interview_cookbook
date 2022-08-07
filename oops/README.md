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