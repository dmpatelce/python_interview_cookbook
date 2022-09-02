# Template Method ##############

The Template method is a Behavioral Design Pattern that defines the skeleton of the operation and leaves the details to be implemented by the child class.  
Its subclasses can override the method implementations as per need but the invocation is to be in the same way as defined by an abstract class.  
The template pattern defines the skeleton of an algorithm in an operation deferring some steps to sub-classes. The template method lets subclasses redefine certain steps of an algorithm without changing the algorithm structure.  
So, ultimately we have one template class and template methods with proper sequence of execution and all the subclasses will also follow the same template.

## Advantage

- Equivalent Content: It’s easy to consider the duplicate code in the superclass by pulling it there where you want to use it.
- Flexibility: It provides vast flexibility such that subclasses are able to decide how to implement the steps of the algorithms.
- Possibility of Inheritance: We can reuse our code as the Template Method uses inheritance which provides the ability of code reusability.

## Disadvantage

- Hard to debug the code
- Complex Code: The code may become enough complex sometimes while using the template method such that it becomes too much hard to understand the code even by the developers who are writing it.
- Limitness: Clients may ask for the extended version because sometimes they feel lack of algorithms in the provided skeleton.
- Violation: It might be possible that by using Template method, you may end up with violating the Liskov Substitution Principle which is definitely not the good thing to follow.

```python
'''
Template method Pattern - This is behavioral design pattern.
'''
import abc

class ThreeDaysTrip(metaclass=abc.ABCMeta):
    @abc.abstractmethod
    def transport(self):
        pass

    @abc.abstractmethod
    def day1(self):
        pass

    @abc.abstractmethod
    def day2(self):
        pass

    @abc.abstractmethod
    def day3(self):
        pass

    @abc.abstractmethod
    def back_to_home(self):
        pass

    def iternary(self):
        print("Trip is started")
        self.transport()
        self.day1()
        self.day2()
        self.day3()
        self.back_to_home()
        print("Trip is over")


class SouthTrip(ThreeDaysTrip):
    def transport(self):
        print("Go by train! check in to hotel")

    def day1(self):
        print("Day-1: Enjoy the hotel beach whole day")

    def day2(self):
        print("Day-2: Visit historical places and Enjoy cruise life at night")

    def day3(self):
        print("Day-3: Enjoy shopping day with family and go anywhere you wish")

    def back_to_home(self):
        print("Check out and go Home by air!")


class NorthTrip(ThreeDaysTrip):
    def transport(self):
        print("Go by air! check in to hotel")

    def day1(self):
        print("Day-1: Go to very highted place and enjoy snow activities")

    def day2(self):
        print("Day-2: Enjoy river rafting and lavish dinner at night")

    def day3(self):
        print("Day-3: Enjoy shopping day with family and go anywhere you wish")

    def back_to_home(self):
        print("Check out and go Home by air!")


if __name__ == "__main__":
    place = input("Where do you want to go? ")
    if place == 'north':
        trip = NorthTrip()
        trip.iternary()
    elif place == 'south':
        trip = SouthTrip()
        trip.iternary()
    else:
        print("Sorry, We do not have any trip towards that place!")
```