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

In simple words, abstraction means hiding unnecessary details and showing
only what is important. It helps us use something without knowing all the
complex work happening behind the scenes.

Let's take a real-world example.

Think about using an ATM machine. When you want to withdraw money, you only
do a few simple steps:

* insert your card
* enter your PIN
* choose withdraw option
* enter amount
* collect cash

That's it.

But behind the scenes, many things happen. The ATM checks your card,
verifies your PIN, talks to the bank server, checks your balance, updates
your account, prints a receipt, and then gives you cash.

As a user, you do not need to understand all this internal logic. You only
see a simple interface. That is abstraction. It hides the complicated
process and gives you a simple way to use it. In programming, abstraction
works in the same way. We create simple methods for the outside world, and
we hide the complex logic inside the class.

Let's understand this with a simple `FoodOrder` example. Imagine we are
building a food delivery app. The user only wants to place an order. They
do not care about every internal step like checking restaurant
availability, calculating delivery charges, applying discount, assigning
delivery partner, and sending confirmation. So we can create a simple
method called `place_order()`.

```python
class FoodOrder:
    def place_order(self, food_item, user_location):
        self._check_restaurant_availability(food_item)
        self._calculate_delivery_charge(user_location)
        self._apply_discount()
        self._assign_delivery_partner()
        self._send_confirmation()
        print(f"Your order for {food_item} has been placed successfully.")

    def _check_restaurant_availability(self, food_item):
        print(f"Checking restaurant availability for {food_item}")

    def _calculate_delivery_charge(self, user_location):
        print(f"Calculating delivery charge for {user_location}")

    def _apply_discount(self):
        print("Applying available discount.")

    def _assign_delivery_partner(self):
        print("Assigning delivery partner.")

    def _send_confirmation(self):
        print("Sending order confirmation.")
```

Now the outside code can use it like this:

```python
order = FoodOrder()
order.place_order("Pizza", "Delhi")
```

The user of this class only calls one simple method:

`place_order()`

They do not need to call all the small internal methods one by one.

They do not need to know how the restaurant is checked.

They do not need to know how delivery charge is calculated.

They do not need to know how the delivery partner is assigned.

All those details are hidden inside the class. This is abstraction. We
expose only the important action and hide the complex steps behind it.
This makes the code easier to use. It also makes the code easier to
change. For example, tomorrow if we want to change how delivery partners
are assigned, we can update the internal `_assign_delivery_partner()`
method.

The outside code will still call the same `place_order()` method. Nothing
changes for the user of the class. That is the beauty of abstraction. It
gives a simple outside view and hides the complex inside work.

So remember this simple line:

Abstraction hides complexity and shows only what is necessary.
Encapsulation protects the internal data. Abstraction hides the internal
process. Both are related, but they solve different problems.

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
