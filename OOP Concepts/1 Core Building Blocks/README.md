# Core Building Blocks

Object-Oriented Programming (OOP) organizes code around *things* rather than
just steps.

## 1. Class

A class is like a plan or a blueprint — it defines what data (attributes) and behavior
(methods) its instances will have.

<img width="1100" height="619" alt="image" src="https://github.com/user-attachments/assets/35512d2f-2c16-4f43-951b-aab40dacedc1" />

For example, think about a car.

A car has some information:
* brand
* color
* speed

And a car can do some actions:
* start
* stop
* increase speed

So, if we want to represent a car in code, we create a Car class.

```python
class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color
        self.speed = 0

    def start(self):
        print(f"{self.brand} car has started.")

    def increase_speed(self, value):
        self.speed = self.speed + value
        print(f"Current speed: {self.speed} km/h")

    def get_details(self):
        return f"{self.brand} - {self.color}"
```

In this example, Car is a class. It defines what a car should have and what a car can do.
It contains data like brand, color, and speed.
It also contains actions like start(), increaseSpeed(), and getDetails().

So instead of keeping car data in random variables and writing separate functions outside, we keep related data and related behavior together inside one class.

A simple real-life example is a house blueprint. A blueprint shows where the rooms, doors, windows, and walls should be.
But you cannot live inside a blueprint. You need to build an actual house from it.

In the same way, a class is only a blueprint. It only defines the structure. 

***NOTE***: It doesn't exist as a "thing" in
memory until you create an object from it.

```python
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author
```

## 2. Object

An object (or instance) is a concrete realization of a class — actual data
in memory that follows the shape the class defines. You can create many
objects from a single class, each with its own state.

We created a Car class in the previous section. That Car class only defines what a car should have and what a car can do.

<img width="1100" height="619" alt="image" src="https://github.com/user-attachments/assets/9400420b-2338-4c58-b810-474beac96f69" />

It says a car can have:
* brand
* color
* speed

And it can do actions like:
* start
* stop
* increase speed

But the class itself is not a real car. To use it, we need to create objects from it. Here is an example:

```python
car1 = Car("Toyota", "Red")
car2 = Car("Honda", "Blue")
car3 = Car("Tesla", "Black")
```

Here, car1, car2, and car3 are objects. All three objects are created from the same Car class. But each object has its own values.

"    " car1 is a red Toyota.

"    " car2 is a blue Honda.

"    " car3 is a black Tesla.

Now we can use these objects like this:

```python
car1.start()
car1.increase_speed(40)
car2.start()
car2.increase_speed(60)
car3.start()
car3.increase_speed(80)
```

## 3. Attributes (Fields / Properties)

Attributes are the data a class stores — the variables attached to each
object. They represent the *state* of an object at any given moment
(`title`, `author` above).

## 4. Methods

Methods are functions defined on a class that operate on its attributes.
They represent the *behavior* an object can perform.

```python
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author

    def describe(self):
        return f"{self.title} by {self.author}"
```

## 5. Constructor

The constructor is the special method that runs when an object is created.
It's responsible for setting up an object's initial state. In Python this
is `__init__`; in Java/C# it's a method with the same name as the class.

## Why this matters

Classes and objects let you model real-world (or domain) concepts directly
in code: a `Book`, a `User`, an `Order`. Attributes capture what an object
*is*, methods capture what it *does*, and the constructor guarantees every
object starts in a valid state.
