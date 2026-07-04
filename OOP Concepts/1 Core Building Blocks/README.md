# Core Building Blocks

Object-Oriented Programming (OOP) organizes code around *things* rather than
just steps. These are the foundational pieces every OOP language builds on.

## 1. Class

A class is a blueprint — it defines what data (attributes) and behavior
(methods) its instances will have, but it doesn't exist as a "thing" in
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

```python
book1 = Book("Dune", "Frank Herbert")
book2 = Book("Piranesi", "Susanna Clarke")
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
