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
It is a has-a relationship, where one class contains references to other objects, but those objects can exist independently of the container. 
It's a whole-part relationship with weak ownership.

<img width="1100" height="880" alt="image" src="https://github.com/user-attachments/assets/3c1fbb91-7455-43e2-acd0-560f4eb93988" />

Let's understand this with a simple real-world example.

Think about a school and teachers. A school has many teachers. But
teachers can exist without that school. If a school closes, the teachers
do not disappear. They can join another school. So the school has
teachers, but it does not fully control the life of the teachers. That is
aggregation.

Let's see this in Python:

```python
class School:
    def __init__(self, name):
        self.name = name
        self.teachers = []

    def add_teacher(self, teacher):
        self.teachers.append(teacher)

    def show_teachers(self):
        print(f"Teachers in {self.name}:")
        for teacher in self.teachers:
            print(teacher.get_name())
```

Now we create a `Teacher` class:

```python
class Teacher:
    def __init__(self, name, subject):
        self.name = name
        self.subject = subject

    def get_name(self):
        return f"{self.name} teaches {self.subject}"
```

Now let's use both classes:

```python
teacher1 = Teacher("Mr. Sharma", "Math")
teacher2 = Teacher("Ms. Verma", "Science")

school = School("Green Valley School")
school.add_teacher(teacher1)
school.add_teacher(teacher2)
school.show_teachers()
```

Here, the `Teacher` objects are created outside the `School` class. After
that, we add them to the school. This is important. The school is not
creating the teachers internally. The teachers already exist, and the
school is only keeping a reference to them. That means teachers can still
exist even if the school object is removed. For example, the same teacher
can join another school:

```python
another_school = School("Sunrise Public School")
another_school.add_teacher(teacher1)
```

Here, `teacher1` can be reused in another school. This shows that the
teacher has its own independent life. That is the main idea of
aggregation. The whole object has parts, but the parts can survive
without the whole.

Some more examples:

* A department has employees.
* A library has books.
* A team has players.
* A school has teachers.

In all these examples, the smaller objects can still exist even if the
bigger object is removed.

So remember this simple line:

Aggregation means one object has another object, but the child object can
still exist independently. In association, objects are just connected. In
aggregation, one object has another object. But the ownership is still
weak.

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

<img width="1100" height="877" alt="image" src="https://github.com/user-attachments/assets/da90bcd7-d6c8-40ac-ab14-86d5ba867564" />

In simple words, dependency means one class uses another class for a short time. It is a temporary relationship. 
One class does not own the other class. It also does not keep the other class permanently inside itself. 
It only uses it when needed. That is why dependency is considered the weakest relationship between classes.

[insert here]

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
