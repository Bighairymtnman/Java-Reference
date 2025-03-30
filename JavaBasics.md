# Java Basics Quick Reference

## Table of Contents
- [Classes and Objects](#classes-and-objects)
- [Inheritance](#inheritance)
- [Interfaces](#interfaces)
- [Abstract Classes](#abstract-classes)
- [Polymorphism](#polymorphism)
- [Encapsulation](#encapsulation)

## Classes and Objects
```java
// Basic Class Structure
public class Car {
    // Instance variables (attributes)
    private String brand;        // Private for encapsulation
    private int year;
    public boolean isRunning;    // Public attribute

    // Constructor - creates new Car objects
    public Car(String brand, int year) {
        this.brand = brand;      // 'this' refers to current instance
        this.year = year;
        this.isRunning = false;
    }

    // Method to start the car
    public void startEngine() {
        isRunning = true;
        System.out.println("Engine started!");
    }

    // Getter method - allows safe access to private data
    public String getBrand() {
        return brand;
    }

    // Setter method - allows controlled modification
    public void setYear(int year) {
        if (year > 1900) {       // Data validation
            this.year = year;
        }
    }
}

// Creating and Using Objects
Car myCar = new Car("Toyota", 2020);    // Create new Car
myCar.startEngine();                    // Call method
String brand = myCar.getBrand();        // Use getter
```

## Inheritance
```java
// Parent (Base) Class
public class Animal {
    protected String name;       // 'protected' allows access in child classes
    
    // Constructor
    public Animal(String name) {
        this.name = name;
    }
    
    // Method that can be inherited
    public void makeSound() {
        System.out.println("Some sound");
    }
}

// Child (Derived) Class
public class Dog extends Animal {    // 'extends' indicates inheritance
    private String breed;            // Additional attribute

    // Child constructor
    public Dog(String name, String breed) {
        super(name);                 // Call parent constructor
        this.breed = breed;
    }

    // Override parent's method
    @Override                        // Good practice to use @Override
    public void makeSound() {
        System.out.println("Woof!");
    }

    // Additional method specific to Dog
    public void fetch() {
        System.out.println(name + " is fetching!");
    }
}

// Using Inheritance
Dog myDog = new Dog("Rex", "Labrador");
myDog.makeSound();              // Uses overridden method
myDog.fetch();                  // Uses Dog-specific method
```

## Interfaces
```java
// Interface Definition
public interface Flyable {
    // Abstract methods (no implementation)
    void fly();                     // Implicitly public and abstract
    void land();

    // Default method (Java 8+)
    default void glide() {          // Provides default implementation
        System.out.println("Gliding in air");
    }

    // Static method in interface
    static int getWingCount() {
        return 2;
    }
}

// Class implementing interface
public class Bird implements Flyable {
    // Must implement all abstract methods
    @Override
    public void fly() {
        System.out.println("Bird is flying");
    }

    @Override
    public void land() {
        System.out.println("Bird has landed");
    }
    
    // Can use default method as-is or override it
}

// Multiple Interface Implementation
public class Airplane implements Flyable, Maintainable {
    // Must implement all methods from both interfaces
}
```

## Abstract Classes
```java
// Abstract Class Definition
public abstract class Shape {
    protected String color;         // Common attribute

    // Constructor in abstract class
    public Shape(String color) {
        this.color = color;
    }

    // Abstract method (must be implemented by children)
    public abstract double calculateArea();

    // Concrete method (shared implementation)
    public void displayColor() {
        System.out.println("Color is " + color);
    }
}

// Concrete Class extending Abstract Class
public class Circle extends Shape {
    private double radius;

    public Circle(String color, double radius) {
        super(color);              // Call abstract class constructor
        this.radius = radius;
    }

    // Must implement abstract method
    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}
```

## Polymorphism
```java
// Polymorphic Class Structure
public class Vehicle {
    public void move() {
        System.out.println("Vehicle is moving");
    }
}

public class Car extends Vehicle {
    @Override
    public void move() {
        System.out.println("Car is driving");
    }
}

public class Boat extends Vehicle {
    @Override
    public void move() {
        System.out.println("Boat is sailing");
    }
}

// Polymorphic Method Usage
public class Transportation {
    // Polymorphic method - accepts any Vehicle type
    public void startJourney(Vehicle vehicle) {
        vehicle.move();            // Calls appropriate version
    }

    public static void main(String[] args) {
        Transportation t = new Transportation();
        
        // Same method, different behaviors
        t.startJourney(new Car());     // "Car is driving"
        t.startJourney(new Boat());    // "Boat is sailing"
    }
}
```

## Encapsulation
```java
// Fully Encapsulated Class
public class BankAccount {
    // Private attributes
    private String accountNumber;
    private double balance;
    private String ownerName;

    // Constructor
    public BankAccount(String accountNumber, String ownerName) {
        this.accountNumber = accountNumber;
        this.ownerName = ownerName;
        this.balance = 0.0;
    }

    // Public methods to access private data
    public double getBalance() {
        return balance;
    }

    // Controlled data modification
    public void deposit(double amount) {
        if (amount > 0) {          // Validation
            balance += amount;
        }
    }

    public boolean withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            return true;
        }
        return false;
    }

    // Private helper method
    private void notifyOwner(String message) {
        // Internal implementation
        System.out.println("Notification to " + ownerName + ": " + message);
    }
}

// Using Encapsulated Class
BankAccount account = new BankAccount("123456", "John Doe");
account.deposit(1000);         // Controlled access
double balance = account.getBalance();  // Safe data access
```
