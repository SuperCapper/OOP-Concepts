# The 4 Pillars That Make OOP Powerful

These four principles are what separate OOP from simply grouping functions
and data together. Together they make code easier to change, extend, and
reason about.

## 1. Encapsulation

[Insert here]

***

Encapsulation means bundling data and the methods that operate on it inside
a single unit (a class), and hiding internal details from the outside world.
Callers interact with an object through its public interface, not by
reaching into its internals directly.

```python
class Account:
    def __init__(self, balance):
        self._balance = balance          # "private" by convention

    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Deposit must be positive")
        self._balance += amount

    def get_balance(self):
        return self._balance
```

**Why it matters:** it protects an object's internal state from being put
into an invalid state by outside code, and lets you change the
implementation later without breaking callers.

## 2. Abstraction

Abstraction means exposing only the essential behavior of an object while
hiding the complexity of how it works. A caller can call `car.start()`
without knowing anything about fuel injection or ignition timing.

```python
from abc import ABC, abstractmethod

class PaymentMethod(ABC):
    @abstractmethod
    def pay(self, amount):
        ...

class CreditCard(PaymentMethod):
    def pay(self, amount):
        print(f"Charging ${amount} to credit card")
```

**Why it matters:** it reduces cognitive load — you work with a simple,
stable interface instead of every implementation detail.

## 3. Inheritance

Inheritance lets a class (the *subclass*/*child*) reuse and extend the
attributes and methods of another class (the *superclass*/*parent*),
modeling an "is-a" relationship.

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return "..."

class Dog(Animal):
    def speak(self):
        return "Woof!"
```

**Why it matters:** it avoids duplicating shared logic across related
classes, and establishes a natural hierarchy (a `Dog` *is an* `Animal`).

## 4. Polymorphism

Polymorphism means objects of different classes can be treated through a
common interface, with each responding to the same method call in its own
way.

```python
animals = [Dog("Rex"), Cat("Whiskers")]
for a in animals:
    print(a.speak())   # each subclass provides its own behavior
```

**Why it matters:** calling code doesn't need to know the exact type it's
working with — it just needs to know the object supports a given method,
which makes systems easier to extend with new types.

## How the four pillars work together

- **Encapsulation** protects state.
- **Abstraction** simplifies what's exposed.
- **Inheritance** shares structure and behavior between related classes.
- **Polymorphism** lets that shared interface be used interchangeably.

Together they're the reason OOP code can grow in complexity without
becoming unmanageable.
