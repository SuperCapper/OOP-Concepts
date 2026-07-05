# Object Relationships: How Classes Work Together

Real programs are made of many classes cooperating, not just standalone
hierarchies. These relationships describe *how* objects reference and
depend on one another.

## 1. Association

A general relationship where one class uses or interacts with another, without owning it.
In simple words, association means one object knows about another object. 
Both objects are connected, but they can still exist independently. One object does not fully own the other object.

<img width="1100" height="825" alt="image" src="https://github.com/user-attachments/assets/7551207b-5204-4794-8dde-9756d30687ab" />

Let's take a simple real-world example.

Think about a teacher and a student. A teacher can teach many students. A
student can learn from many teachers. But both can exist separately. If
one student leaves the class, the teacher still exists. If one teacher
leaves the school, the student can still learn from another teacher. So
the relationship is there, but ownership is not strong.

That is association.

Let's see this in Python:

```python
class Teacher:
    def __init__(self, name):
        self.name = name
        self.students = []

    def add_student(self, student):
        self.students.append(student)

    def show_students(self):
        print(f"{self.name} teaches:")
        for student in self.students:
            print(student.name)
```

Now we create a `Student` class:

```python
class Student:
    def __init__(self, name):
        self.name = name
```

Now we can connect teacher and student objects:

```python
teacher = Teacher("Mr. Sharma")

student1 = Student("Aman")
student2 = Student("Priya")

teacher.add_student(student1)
teacher.add_student(student2)
teacher.show_students()
```

Here, `Teacher` and `Student` are two separate objects. The teacher object
knows about the student objects. But the students are not completely
owned by the teacher. They are created separately. That means they can
exist even outside the `Teacher` class. This is the main point of
association. Objects are connected, but they are still independent.

You can think of association like this:

* A teacher teaches students.
* A doctor treats patients.
* A driver drives a car.
* A customer places an order.

In all these examples, objects are related, but one object does not
fully control the lifecycle of the other object.

So remember this simple line:

Association means one object is connected to another object, but both
can live independently. Association is the most general relationship
between objects.

## 2. Aggregation

Aggregation is a special type of association. 
In simple words, aggregation means one object has another object, but the child object can still live independently. 
It is a has-a relationship, but not a very strict one.

<img width="1100" height="880" alt="image" src="https://github.com/user-attachments/assets/3c1fbb91-7455-43e2-acd0-560f4eb93988" />

[insert here]

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
