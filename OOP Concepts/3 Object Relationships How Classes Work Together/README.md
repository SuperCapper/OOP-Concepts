# Object Relationships: How Classes Work Together

Real programs are made of many classes cooperating, not just standalone
hierarchies. These relationships describe *how* objects reference and
depend on one another.

## 1. Association

A general relationship where one class uses or interacts with another, without owning it.
In simple words, association means one object knows about another object. 
Both objects are connected, but they can still exist independently. One object does not fully own the other object.

<img width="1100" height="825" alt="image" src="https://github.com/user-attachments/assets/7551207b-5204-4794-8dde-9756d30687ab" />

[insert here]



```python
class Teacher:
    def teach(self, student):
        print(f"Teaching {student.name}")
```

A `Teacher` and a `Student` are associated, but neither owns the other's
lifecycle.

## 2. Aggregation

A "has-a" relationship where one class contains references to other
objects, but those objects can exist independently of the container. It's
a whole-part relationship with weak ownership.

```python
class Library:
    def __init__(self):
        self.books = []   # Books can exist even if the Library doesn't

    def add_book(self, book):
        self.books.append(book)
```

If the `Library` is deleted, the `Book` objects it referenced can still
exist elsewhere.

## 3. Composition

A stronger "has-a" relationship where the contained object's lifecycle is
tied to the containing object — if the whole is destroyed, so are its
parts.

```python
class Engine:
    def start(self):
        print("Engine starting")

class Car:
    def __init__(self):
        self.engine = Engine()   # Engine is created and owned by Car

    def start(self):
        self.engine.start()
```

The `Engine` here has no meaningful existence outside its `Car`.

## 4. Dependency

A weaker, often temporary relationship where one class uses another,
typically just within a method, without storing a long-term reference to
it.

```python
class OrderProcessor:
    def process(self, payment_gateway, order):
        payment_gateway.charge(order.total)   # used, not stored
```

`OrderProcessor` depends on a `payment_gateway` only for the duration of
`process()` — it doesn't hold onto it as part of its own state.

## Association vs. Aggregation vs. Composition vs. Dependency

| Relationship | Ownership | Lifecycle tied? | Example |
|---|---|---|---|
| Association | None | No | Teacher ↔ Student |
| Aggregation | Weak ("has-a") | No | Library → Books |
| Composition | Strong ("has-a") | Yes | Car → Engine |
| Dependency | None (transient use) | No | OrderProcessor uses PaymentGateway |

## Why this matters

Inheritance (from the 4 pillars) models "is-a" relationships. These four
relationships model "has-a" and "uses-a" relationships — and most
real-world object models are built primarily from composition and
association rather than deep inheritance trees.
