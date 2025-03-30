# Python Basics Quick Reference

## Table of Contents
- [Classes and Objects](#classes-and-objects)
- [Inheritance](#inheritance)
- [Abstract Classes](#abstract-classes)
- [Polymorphism](#polymorphism)
- [Encapsulation](#encapsulation)
- [Special Methods](#special-methods)

## Classes and Objects
```python
# Basic Class Structure
class Car:
    # Class variable (shared by all instances)
    total_cars = 0
    
    # Constructor (initialize instance)
    def __init__(self, brand: str, year: int):
        self.brand = brand      # Public attribute
        self._year = year       # Protected attribute (convention)
        self.__running = False  # Private attribute (name mangling)
        Car.total_cars += 1     # Access class variable
    
    # Instance method
    def start_engine(self):
        self.__running = True
        print("Engine started!")
    
    # Property decorator (getter)
    @property
    def year(self):
        return self._year
    
    # Property setter
    @year.setter
    def year(self, value):
        if value > 1900:        # Data validation
            self._year = value
    
    # Class method (works with class itself)
    @classmethod
    def get_total_cars(cls):
        return cls.total_cars
    
    # Static method (utility function)
    @staticmethod
    def validate_brand(brand):
        return bool(brand and brand.strip())

# Creating and Using Objects
my_car = Car("Toyota", 2020)    # Create new Car
my_car.start_engine()           # Call method
year = my_car.year              # Use property
my_car.year = 2021             # Use setter
total = Car.get_total_cars()    # Use class method
```

## Inheritance
```python
# Parent Class
class Animal:
    def __init__(self, name: str):
        self.name = name
    
    def make_sound(self):
        print("Some sound")
    
    # Method meant to be overridden
    def move(self):
        raise NotImplementedError("Subclass must implement")

# Child Class
class Dog(Animal):              # Inherit from Animal
    def __init__(self, name: str, breed: str):
        super().__init__(name)  # Call parent constructor
        self.breed = breed
    
    # Override parent's method
    def make_sound(self):
        print("Woof!")
    
    # Implement required method
    def move(self):
        print("Running on four legs")
    
    # Additional method
    def fetch(self):
        print(f"{self.name} is fetching!")

# Multiple Inheritance
class Pet:
    def __init__(self, owner: str):
        self.owner = owner

class FamilyDog(Dog, Pet):      # Multiple inheritance
    def __init__(self, name: str, breed: str, owner: str):
        Dog.__init__(self, name, breed)
        Pet.__init__(self, owner)

# Using Inheritance
my_dog = Dog("Rex", "Labrador")
my_dog.make_sound()             # Uses overridden method
my_dog.fetch()                  # Dog-specific method
```

## Abstract Classes
```python
from abc import ABC, abstractmethod

# Abstract Base Class
class Shape(ABC):
    def __init__(self, color: str):
        self.color = color
    
    @abstractmethod
    def calculate_area(self) -> float:
        """Must be implemented by subclasses"""
        pass
    
    @abstractmethod
    def calculate_perimeter(self) -> float:
        """Must be implemented by subclasses"""
        pass
    
    # Concrete method
    def describe(self):
        print(f"This is a {self.color} shape")

# Concrete Class
class Circle(Shape):
    def __init__(self, color: str, radius: float):
        super().__init__(color)
        self.radius = radius
    
    # Implement abstract methods
    def calculate_area(self) -> float:
        return 3.14159 * self.radius ** 2
    
    def calculate_perimeter(self) -> float:
        return 2 * 3.14159 * self.radius

# Using Abstract Classes
circle = Circle("red", 5)
area = circle.calculate_area()   # Use implemented method
circle.describe()               # Use inherited method
```

## Polymorphism
```python
# Polymorphic Classes
class Vehicle:
    def move(self):
        print("Vehicle moving")

class Car(Vehicle):
    def move(self):
        print("Car driving")

class Boat(Vehicle):
    def move(self):
        print("Boat sailing")

# Duck Typing (Python's approach to polymorphism)
def start_journey(vehicle):
    vehicle.move()              # Will work with any object that has move()

# Using Polymorphism
car = Car()
boat = Boat()

# Same function, different behaviors
start_journey(car)              # "Car driving"
start_journey(boat)             # "Boat sailing"

# Duck Typing Example
class Robot:
    def move(self):
        print("Robot walking")

start_journey(Robot())          # Works because Robot has move()
```

## Encapsulation
```python
# Fully Encapsulated Class
class BankAccount:
    def __init__(self, account_number: str, owner: str):
        self.__account_number = account_number  # Private
        self.__owner = owner                    # Private
        self.__balance = 0.0                    # Private
    
    # Property for read-only access
    @property
    def balance(self) -> float:
        return self.__balance
    
    # Property for read-only access
    @property
    def owner(self) -> str:
        return self.__owner
    
    # Public methods for controlled access
    def deposit(self, amount: float) -> bool:
        if amount > 0:
            self.__balance += amount
            self.__notify_owner("Deposit successful")
            return True
        return False
    
    def withdraw(self, amount: float) -> bool:
        if amount > 0 and amount <= self.__balance:
            self.__balance -= amount
            self.__notify_owner("Withdrawal successful")
            return True
        return False
    
    # Private helper method
    def __notify_owner(self, message: str):
        print(f"Notification to {self.__owner}: {message}")

# Using Encapsulated Class
account = BankAccount("123456", "John Doe")
account.deposit(1000)           # Use public method
balance = account.balance       # Use property
```

## Special Methods
```python
# Class with Special Methods
class Point:
    def __init__(self, x: float, y: float):
        self.x = x
        self.y = y
    
    # String representation
    def __str__(self) -> str:
        return f"Point({self.x}, {self.y})"
    
    # Detailed string representation
    def __repr__(self) -> str:
        return f"Point(x={self.x}, y={self.y})"
    
    # Addition operator
    def __add__(self, other) -> 'Point':
        return Point(self.x + other.x, self.y + other.y)
    
    # Equality comparison
    def __eq__(self, other) -> bool:
        if not isinstance(other, Point):
            return False
        return self.x == other.x and self.y == other.y
    
    # Less than comparison
    def __lt__(self, other) -> bool:
        return self.x < other.x
    
    # Length (magnitude)
    def __len__(self) -> int:
        return int((self.x ** 2 + self.y ** 2) ** 0.5)
    
    # Make object callable
    def __call__(self, factor: float) -> 'Point':
        return Point(self.x * factor, self.y * factor)

# Using Special Methods
p1 = Point(2, 3)
p2 = Point(3, 4)
print(p1)                       # Uses __str__
sum_point = p1 + p2            # Uses __add__
scaled = p1(2)                 # Uses __call__
```
