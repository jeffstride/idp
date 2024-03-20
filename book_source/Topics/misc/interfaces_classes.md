# Interfaces and Classes

In Python, classes and interfaces are fundamental concepts that form the building blocks of `object-oriented programming (OOP)`. This lesson will take a look at classes and interfaces to understand how they work and when to use them. 

## Classes 
````{tab-set} 
```{tab-item} Defining Classes
A class is a blueprint for creating objects in Python. It encapsulates data and the methods that operate on that data. Consider the following example of a simple class:

```python
class Cookie:
    def __init__(self, shape, frosting):
        self.shape = shape
        self.frosting = frosting 

    def display_cookie(self):
        print(f"{self.shape} {self.frosting_flavor} Cookie")

```

```{tab-item} Creating Objects
To use the class, you instantiate objects (instances) from it. All of the cookie objects will have the same essential information such as a shape and a frosting. But they can have their `unique differences` such as a different shape or a different flavor of frosting. 

```python
star_cookie = Cookie("Star", "Cherry")
star_cookie.display_cookie()  # Output: Star Cherry Cookie

heart_cookie = Cookie("Heart", "Chocolate")
heart_cookie.display_cookie()  # Output: Heart Chocolate Cookie
```

```{tab-item} Benifits of Classes 
1. Classes hide the details of state and behavior into a single unit which is known as `encapsulation`. In the case of cookies, the Cookie class encapsulates the details of each cookie, making it easier to manage and understand. 

2. If you have different types of cookies, like SpecialCookie or PremiumCookie, you can use `inheritance` to create new classes that inherit attributes and methods from the base Cookie class. This promotes code reuse and maintains a consistent structure. It also allows you to do less work and be lazy which is something computer scientists are good at. 

3. With classes, you can `abstract` the details of each cookie, allowing you to focus on the high-level features and behaviors. This makes it easier to work with cookies without getting distracted by unnecessary details. 
````


## Interfaces
There isn’t a keyword called `“interface”` in python and so there are two main approaches to defining interfaces: formal interfaces using Abstract Base Classes (ABCs) and informal interfaces using duck typing.

`Abstract Base Classes (ABC)` in Python provide a formal way to define interfaces. With ABCs, you can explicitly declare the functions that subclasses must implement. 

`Duck typing` is an informal approach to interfaces based on object behavior. Instead of relying on explicit declarations, duck typing evaluates objects based on their ability to provide required functions at runtime. The term "duck typing" comes from the saying, "If it looks like a duck, swims like a duck, and quacks like a duck, then it probably is a duck." In programming, duck typing is a style of coding where the type or class of an object is determined by its behavior rather than its explicit type declaration. 
````{tab-set}
```{tab-item} ABC Example
```python
from abc import ABC, abstractmethod

class PacManCharacter(ABC):
     @abstractmethod
    def move(self):
        pass
    
    @abstractmethod
    def eat(self):
        pass


class PacMan(PacManCharacter):
    
    def __init__(self, name, position):
        self.name = name
        self.position = position
    
    def move(self):
        position += 10  # Overriding Parent's method
    
    def eat(self):
        health += 10  # Overriding Parent's method
```
```{tab-item} Duck Typing Example
```python
class PacManCharacter:
    @abstractmethod
    def move(self):
        pass

    @abstractmethod
    def eat(self):
        pass

class PacMan:
    def move(self):
        position += 10

    def eat(self):
        health += 10
```
```{tab-item} Benifits of Interfaces
When we talk about duck typing in Python, it means we focus on what an object can do, not what it's called. If an object can perform certain actions or have specific qualities, we treat it as if it belongs to a certain type, even if it doesn't explicitly say so. This makes Python code flexible and easy to work with, especially when we're not sure about the exact type of an object.

On the other hand, Abstract Base Classes (ABCs) are like blueprints for classes. They lay out the rules for what methods a class should have, but they don't provide the actual implementation. So, if you're creating a game and want all characters to have certain abilities like moving or attacking, you can use ABCs to make sure each character class follows the same rules.

`In simpler terms, duck typing lets us work with objects based on what they can do, while ABCs provide a template for what methods objects should have.`
```

````