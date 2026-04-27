# Function Overloading & Function Overriding 
---

#  Definitions

## Function Overloading

Function overloading means **multiple functions with the same name but different parameters** within the same class or scope.

## Function Overriding

Function overriding occurs when a derived class defines a function with the same name, parameters, and return type as in the base class.

---

#  Why Do These Concepts Exist?

## Overloading:

- Avoids multiple confusing function names
- Improves readability
- Allows same operation with different inputs

## Overriding:

- Enables runtime polymorphism
- Allows child classes to modify inherited behavior
- Supports flexible and extensible design

---

#  Mental Models

## Overloading Mental Model

Think of a **restaurant menu button labeled “Order”**:

- Order(Pizza)
- Order(Burger)
- Order(Drink)

Same name → different inputs → different behavior

---

## Overriding Mental Model

Think of a **base app feature (Login)**:

- Base login = email/password
- Google login overrides behavior
- Apple login overrides behavior

Same function → different class → different behavior

---

#  Syntax

---

## Function Overloading Syntax

```javascript
class Calculator {
  add(a, b) {}
  add(a, b, c) {}
}
```

---

## Function Overriding Syntax

```javascript
class Parent {
  show() {
    console.log("Parent show");
  }
}

class Child extends Parent {
  show() {
    console.log("Child show");
  }
}
```

---

#  FUNCTION OVERLOADING

---

## Basic Example

```javascript
class Printer {
  print(value) {
    console.log(value);
  }

  print(value, format) {
    console.log(`${format}: ${value}`);
  }
}
```

###  Note

In JavaScript, second method overrides first (no real overloading).  
C++ supports true overloading based on parameters.

---

## Correct C++ Concept 

```cpp
class Printer {
public:
    void print(int value) {
        std::cout << value;
    }

    void print(string value) {
        std::cout << value;
    }
};
```

---

##  Step-by-Step Behavior

1. Compiler checks function name
2. Then checks parameter list
3. Matches correct function at compile time
4. No runtime decision needed

---

##  Real-World Example (Calculator System)

```javascript
class Calculator {
  add(a, b) {
    return a + b;
  }

  add(a, b, c) {
    return a + b + c;
  }
}
```

### Use Case:

- Backend math engine
- Multiple input variations for same operation

---

##  Incorrect Example

```javascript
class Test {
  print(a) {}
  print(a) {} //  duplicate definition
}
```

###  Fix:

Use different parameter counts/types (C++ style)

---

##  Common Mistakes

- Same parameter signature repeated
- Assuming JavaScript supports overloading
- Ignoring type differences (C++ matters)

---

##  Key Points

- Same function name
- Different parameter list
- Compile-time decision (C++)
- Improves readability

---

#  FUNCTION OVERRIDING

---

##  Basic Example

```javascript
class Animal {
  speak() {
    console.log("Animal sound");
  }
}

class Dog extends Animal {
  speak() {
    console.log("Bark");
  }
}
```

---

##  Step-by-Step Execution

1. Parent class defines function
2. Child class inherits it
3. Child provides new implementation
4. At runtime, child version is used

---

##  Real-World Example (Payment System)

```javascript
class Payment {
  process() {
    console.log("Processing payment");
  }
}

class PayPalPayment extends Payment {
  process() {
    console.log("Processing PayPal payment");
  }
}
```

### Use Case:

- Different payment gateways
- Same interface, different behavior

---

##  Incorrect Example

```javascript
class Parent {
  show() {}
}

class Child extends Parent {
  show(int a) {} //  not overriding, it's overloading
}
```

---
### Fix

```javascript
class Child extends Parent {
  show() {
    console.log("Overridden method");
  }
}
```

---

##  Common Mistakes

- Changing parameter list (becomes overloading, not overriding)
- Forgetting inheritance
- Ignoring runtime binding rules

---

##  Key Points

- Same function signature
- Different class (inheritance required)
- Runtime polymorphism
- Child replaces parent behavior

---

#  OVERLOADING vs OVERRIDING

|Feature|Overloading|Overriding|
|---|---|---|
|Concept Type|Compile-time polymorphism|Runtime polymorphism|
|Location|Same class|Parent-child classes|
|Parameters|Must differ|Must be same|
|Inheritance needed|No|Yes|
|Binding|Early binding|Late binding|
|Purpose|Flexibility in inputs|Behavior modification|

---

#  Edge Cases & Pitfalls

---

## Overloading Pitfalls

- Only parameter difference matters (C++)
- Return type alone cannot differentiate
- Ambiguous calls cause compiler errors

---

## Overriding Pitfalls

- Signature mismatch breaks override
- Missing virtual keyword in C++
- Accidentally creating overload instead of override

---

#  Internal Behavior (Advanced Insight)

---

## Overloading (Compile-Time Resolution)

- Compiler selects function before execution
- Based on:
    - Number of parameters
    - Types of parameters

---

## Overriding (Runtime Resolution)

- Uses **virtual function table (vtable)** in C++
- Decision happens during execution
- Enables polymorphism

---

#  Real-World Use Cases

---

## 1. Backend API Layer (Overriding)

```javascript
class API {
  request() {
    console.log("Generic request");
  }
}

class AuthAPI extends API {
  request() {
    console.log("Auth request with token");
  }
}
```

### Why:

- Same API structure
- Different services override behavior

---

## 2. Logging System (Overloading Concept)

```javascript
class Logger {
  log(message) {}
  log(message, level) {}
}
```

### Why:

- Same function name
- Different logging formats

---

## 3. Payment Gateway System (Overriding)

- Stripe overrides payment processing
- PayPal overrides payment processing
- Razorpay overrides payment processing

---

#  Mental Model Summary

## Overloading:

> Same name, different inputs → “Multiple ways to do same action”

## Overriding:

> Same function, different class → “Replace behavior in child”

---

#  Key Points

- Overloading = multiple behaviors in same class
- Overriding = modified behavior in subclass
- Overloading is compile-time
- Overriding is runtime
- C++ supports both; JavaScript only simulates them

---

#  Interview Summary

- Overloading: same function name, different parameters
- Overriding: same function signature in derived class
- Overloading = compile-time polymorphism
- Overriding = runtime polymorphism
- Overriding requires inheritance
- C++ uses vtable for overriding internally

---

#  Final Mental Model

- Overloading → “Many forms of input”
- Overriding → “New form of behavior”

---