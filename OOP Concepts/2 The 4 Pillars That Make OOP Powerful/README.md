# The 4 Pillars That Make OOP Powerful

These four principles are what separate OOP from simply grouping functions
and data together. Together they make code easier to change, extend, and
reason about.

## 1. Encapsulation

Encapsulation is one of the most important pillars of OOP. 
Encapsulation means bundling data and the methods that operate on it inside a single unit (a class), 
and hiding internal details from the outside world. 
Callers interact with an object through its public interface, not by reaching into its internals directly.

It is like putting important data inside a safe box. Other people can use
the safe box through proper buttons or keys, but they cannot directly touch
everything inside.

In programming, this helps us protect our object from invalid changes.
Let's understand this with a simple bank account example.

A bank account has some data:

* account holder name
* balance

And it has some actions:

* deposit money
* withdraw money
* check balance

Now imagine if the balance is public and anyone can change it directly.

```python
class BankAccount:
    def __init__(self):
        self.account_holder = None
        self.balance = None
```

Now someone can do this:

```python
account = BankAccount()
account.account_holder = "Shivam"
account.balance = 5000
account.balance = -10000  # Wrong value
```

This is a problem. A real bank account balance should not become negative
like this without any proper rule. But because `balance` is public, anyone
can change it directly. This makes the object unsafe. Now let's use
encapsulation.

```python
class BankAccount:
    def __init__(self, account_holder, opening_balance):
        self._account_holder = account_holder
        if opening_balance >= 0:
            self._balance = opening_balance
        else:
            self._balance = 0

    def deposit(self, amount):
        if amount > 0:
            self._balance += amount
            print(f"Deposited: {amount}")
        else:
            print("Deposit amount must be positive.")

    def withdraw(self, amount):
        if 0 < amount <= self._balance:
            self._balance -= amount
            print(f"Withdrawn: {amount}")
        else:
            print("Invalid withdrawal amount.")

    def get_balance(self):
        return self._balance

    def get_account_holder(self):
        return self._account_holder
```

Now the important data is private.

```python
self._balance
```

*(Python has no true `private` keyword like Java — a leading underscore is
just a convention signaling "internal, don't touch directly.")*

This means no one can directly change the balance from outside the class as
intended. They shouldn't do this anymore:

```python
account.balance = -10000  # Not allowed
```

Instead, they have to use proper methods like:

```python
account = BankAccount("Shivam", 5000)
account.deposit(2000)
account.withdraw(1000)
print(account.get_balance())
```

Now the class controls how the balance changes. If someone tries to deposit
a negative amount, the class can reject it. If someone tries to withdraw
more money than available, the class can stop it. That is the main idea of
encapsulation. We hide the internal data and expose only safe methods to
work with that data.

This makes our code more secure, more controlled, and easier to maintain.
If tomorrow we want to add more rules, like minimum balance, transaction
charges, or daily withdrawal limits, we can add them inside the
`BankAccount` class.

The outside code does not need to know all these internal details. It only
uses simple methods like `deposit()`, `withdraw()`, and `get_balance()`.

So remember this simple line:

Encapsulation protects the data by controlling how it is accessed and
changed. It hides the internal details of a class.

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
