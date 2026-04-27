# Four Pillars of OOP

---

##  Definition

Object-Oriented Programming (OOP) is a programming paradigm based on the concept of **objects**, which bundle **data (variables)** and **behavior (functions)** together.

The **four pillars of OOP** are:

1. **Encapsulation**
2. **Abstraction**
3. **Inheritance**
4. **Polymorphism**

These pillars help structure code in a way that is **modular, reusable, and easier to maintain**.

---

##  Why Do We Need OOP?

Without OOP:

- Code becomes repetitive
- Hard to scale and maintain
- Logic and data are scattered

With OOP:

- Code is **organized into reusable components**
- Easier to **debug and extend**
- Models real-world systems effectively

---

# 1. Encapsulation

---

##  Definition

Encapsulation is the concept of wrapping data members (variables) and member functions (function) together inside a class and restricting direct access to the data.

---

##  Mental Model

Think of a **capsule**:
- Inside: medicine (data)
- Outside: shell (methods controlling access)

You **don’t touch the medicine directly**, you interact through the capsule.

---

##  Why It Exists

- Protects data from accidental modification
- Enforces controlled access
- Improves maintainability

---

##  Syntax (JavaScript)

```javascript
class BankAccount {
  #balance = 0; // private field

  deposit(amount) {
    if (amount > 0) {
      this.#balance += amount;
    }
  }

  getBalance() {
    return this.#balance;
  }
}
```

---

##  Basic Example

```javascript
const acc = new BankAccount();
acc.deposit(100);
console.log(acc.getBalance()); // 100
```

---

##  Incorrect Example

```javascript
class BankAccount {
  balance = 0; // public

  deposit(amount) {
    this.balance += amount;
  }
}

const acc = new BankAccount();
acc.balance = -1000; //  invalid manipulation
```

###  Fix

Use private fields:

```javascript
#balance
```

---

##  Common Mistakes

- Exposing internal variables directly
- Not validating input inside methods

---

## Key Points

- Use private fields (`#`)
- Provide getters/setters
- Validate all inputs

---

##  Interview Tip

Encapsulation = **data hiding + controlled access**

---

# 2. Abstraction

---

##  Definition

Abstraction means **hiding complex implementation details** and showing only essential features.

---

## Mental Model

Driving a car:
- You use **steering & pedals**
- You don’t see engine internals

---

##  Why It Exists

- Reduces complexity
- Improves usability
- Focuses on _what_ instead of _how

---

##  Syntax

JavaScript doesn’t have built-in abstract classes, but we simulate them:

```javascript
class Shape {
  area() {
    throw new Error("Method must be implemented");
  }
}
```

---

##  Example

```javascript
class Circle extends Shape {
  constructor(radius) {
    super();
    this.radius = radius;
  }

  area() {
    return Math.PI * this.radius ** 2;
  }
}
```

---

##  Step-by-Step Breakdown

1. Create base class (`Shape`)
2. Define method placeholder (`area`)
3. Force subclasses to implement it
4. Hide actual logic from user

---

##  Incorrect Example

```javascript
class Shape {
  area() {
    return 0; //  meaningless default
  }
}
```

---

## Common Mistakes

- Providing default implementations when they shouldn't exist
- Not enforcing method overrides

---

##  Key Points

- Focus on **interface**, not implementation
- Use base classes to define structure
- Throw errors for unimplemented methods

---

##  Interview Tip

Abstraction = **Hide complexity, expose essentials**

---

# 3. Inheritance

---

##  Definition

Inheritance is a mechanism in which a derived class(Child Class) acquires the properties of base class (Parent class)

---

##  Mental Model

Parent → Child relationship:
- Child inherits traits from parent
- Can add or modify behavior

---

##  Why It Exists

- Code reuse
- Logical hierarchy
- Reduces duplication

---

## Syntax

```javascript
class Animal {
  speak() {
    console.log("Animal makes sound");
  }
}

class Dog extends Animal {
  speak() {
    console.log("Dog barks");
  }
}
```

---

##  Example

```javascript
const d = new Dog();
d.speak(); // Dog barks
```

---

##  Step-by-Step Breakdown

1. Define parent class
2. Use `extends` keyword
3. Override methods if needed

---

##  Incorrect Example

```javascript
class Dog extends Animal {
  constructor(name) {
    this.name = name; //  must call super()
  }
}
```

 Fix

```javascript
constructor(name) {
  super();
  this.name = name;
}
```

---

##  Common Mistakes

- Forgetting `super()`
- Overusing inheritance (deep hierarchies)

---

##  Key Points

- Use `extends`
- Call `super()` in constructor
- Prefer composition when needed

---

##  Interview Tip

Inheritance = **“is-a” relationship**
Example: Dog **is an** Animal

---

# 4. Polymorphism

---

##  Definition

Polymorphism means **one interface, multiple implementations**.

---

##  Mental Model

Same action, different behavior:
- Button click → different outcomes
- Same method → different outputs

---

##  Why It Exists

- Flexibility
- Extensibility
- Cleaner code

---

##  Syntax

```javascript
class Animal {
  speak() {
    console.log("Animal sound");
  }
}

class Cat extends Animal {
  speak() {
    console.log("Meow");
  }
}

class Dog extends Animal {
  speak() {
    console.log("Bark");
  }
}
```

---

##  Example

```javascript
const animals = [new Cat(), new Dog()];

animals.forEach(a => a.speak());
```

### Output:

```
Meow
Bark
```

---

##  Step-by-Step Breakdown

1. Define common method in base class
2. Override in subclasses
3. Call same method dynamically

---

##  Incorrect Example

```javascript
if (animal.type === "dog") {
  // do dog logic
} else if (animal.type === "cat") {
  // do cat logic
}
```

###  Fix

Use polymorphism instead of conditionals.

---

##  Common Mistakes

- Using conditionals instead of polymorphism
- Not overriding methods properly

---

##  Key Points

- Same method name
- Different behavior
- Works via method overriding

---

##  Interview Tip

Polymorphism = **same interface, different behavior**

---

#  Comparison Table

|Pillar|Focus|Key Benefit|Example Concept|
|---|---|---|---|
|Encapsulation|Data hiding|Security|Private variables|
|Abstraction|Simplicity|Reduced complexity|Abstract classes|
|Inheritance|Reusability|Code reuse|`extends`|
|Polymorphism|Flexibility|Dynamic behavior|Method overriding|

---

#  Real-World Use Cases

---

## 1. Backend (API Design)

```javascript
class Payment {
  process() {
    throw new Error("Implement");
  }
}

class StripePayment extends Payment {
  process() {
    console.log("Processing via Stripe");
  }
}
```

- Abstraction: common interface
- Polymorphism: multiple payment methods
- Encapsulation: hide API keys

---

## 2. Frontend (UI Components)

```javascript
class Button {
  render() {
    console.log("Render button");
  }
}

class IconButton extends Button {
  render() {
    console.log("Render icon button");
  }
}
```

- Inheritance: shared UI logic
- Polymorphism: different rendering

---

#  Edge Cases & Pitfalls

- Deep inheritance chains → hard to debug    
- Over-encapsulation → unnecessary complexity
- Misusing abstraction → vague interfaces
- Ignoring composition → rigid design

---

# Final Mental Model

- **Encapsulation** → Protect data
- **Abstraction** → Hide complexity
- **Inheritance** → Reuse code    
- **Polymorphism** → Flexible behavior
 

---

#  Interview Summary

- OOP is about structuring code using objects
- Four pillars work **together**, not separately
- Always explain with **real-world analogy**
    
- Mention:
    - Encapsulation = data hiding
    - Abstraction = hiding complexity   
    - Inheritance = reuse        
    - Polymorphism = flexibility       
