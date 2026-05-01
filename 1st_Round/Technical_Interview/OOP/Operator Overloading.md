# Operator Overloading in C++ (OOP Perspective)

---

## 1. Definition

**Operator overloading** in C++ allows you to redefine how operators (like `+`, `-`, `==`, etc.) behave for **user-defined types (objects)**.

> It lets objects behave like built-in types in expressions.

---

## 2. Why Operator Overloading Exists

Without operator overloading:

- You must use function calls instead of natural expressions
    
- Code becomes less readable and less intuitive
    

With operator overloading:

- Objects can use operators like numbers
    
- Improves **code readability and expressiveness**
    
- Enables **natural syntax for complex data types**
    

---

## 3. Mental Model

Think of operators as **actions**:

- `+` → add
    
- `==` → compare
    

Operator overloading lets you **teach objects how to respond** to these actions.

---

## 4. Syntax (Concept in JS Style)

```javascript
class NumberWrapper {
  constructor(value) {
    this.value = value;
  }

  add(other) {
    return new NumberWrapper(this.value + other.value);
  }
}
```

---

## 5. C++ Equivalent Syntax

```cpp
class ClassName {
public:
    ReturnType operator op (parameters);
};
```

Example:

```cpp
Complex operator + (const Complex& obj);
```

---

## 6. Basic Example (Addition)

```javascript
class Complex {
  constructor(real, imag) {
    this.real = real;
    this.imag = imag;
  }

  add(other) {
    return new Complex(
      this.real + other.real,
      this.imag + other.imag
    );
  }
}

const c1 = new Complex(2, 3);
const c2 = new Complex(1, 4);

const result = c1.add(c2);
console.log(result); // (3, 7)
```

---

## 7. Step-by-Step Breakdown

```text
c1 = (2,3)
c2 = (1,4)

Add:
real = 2 + 1 = 3
imag = 3 + 4 = 7

Result = (3,7)
```

---

## 8. Intermediate Example (Comparison)

```javascript
class Box {
  constructor(value) {
    this.value = value;
  }

  isEqual(other) {
    return this.value === other.value;
  }
}

const b1 = new Box(10);
const b2 = new Box(10);

console.log(b1.isEqual(b2)); // true
```

---

## 9. Real-World Example (Money System)

```javascript
class Money {
  constructor(amount) {
    this.amount = amount;
  }

  add(other) {
    return new Money(this.amount + other.amount);
  }
}

const m1 = new Money(100);
const m2 = new Money(50);

console.log(m1.add(m2).amount); // 150
```

---

## 10. Real-World Example (Vector Math - Backend/Graphics)

```javascript
class Vector {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  add(v) {
    return new Vector(this.x + v.x, this.y + v.y);
  }
}
```

---

## 11. Internal Behavior (C++ Insight)

When you write:

```cpp
c1 + c2;
```

It internally becomes:

```cpp
c1.operator+(c2);
```

---

## 12. Common Operators You Can Overload

- Arithmetic → `+`, `-`, `*`, `/`
    
- Comparison → `==`, `!=`, `<`
    
- Assignment → `=`
    
- Increment → `++`
    
- Stream → `<<`, `>>`
    

---

## 13. Incorrect Example

```javascript
add(other) {
  return this.value + other; // ❌ wrong type
}
```

### Problem:

- Mixing object with primitive
    

---

### ✔ Fix

```javascript
return new NumberWrapper(this.value + other.value);
```

---

## 14. Common Mistakes

---

### ❌ Breaking operator meaning

Overloading `+` to subtract values

✔ Fix:  
Maintain **expected behavior**

---

### ❌ Returning wrong type

```javascript
return this.value + other.value; // returns number
```

✔ Fix:  
Return object

---

### ❌ Overloading unnecessarily

✔ Fix:  
Use only when it improves clarity

---

## 15. Edge Cases

- Operator precedence issues
    
- Chained operations
    
- Const correctness in C++
    
- Overloading assignment carefully
    

---

## 16. Key Points

- Gives custom meaning to operators
    
- Works only with user-defined types
    
- Improves readability
    
- Should follow logical behavior
    

---

## 17. Comparison: Function vs Operator Overloading

|Feature|Function Call|Operator Overloading|
|---|---|---|
|Syntax|`add(a, b)`|`a + b`|
|Readability|Medium|High|
|Flexibility|High|Controlled|

---

## 18. Real-World Use Cases

---

### 1. Financial Systems

```javascript
balance = deposit + withdrawal;
```

---

### 2. Game Development

- Position vectors
    
- Physics calculations
    

---

## 19. Advanced Insight

- Can overload as:
    
    - Member function
        
    - Friend function
        
- Some operators cannot be overloaded:
    
    - `::`, `.`, `?:`, `sizeof`
        

---

## 20. Interview Tips

---

### What Interviewers Expect:

- Syntax understanding
    
- Operator function mapping
    
- Use cases
    
- Limitations
    

---

### Common Questions:

- What is operator overloading?
    
- Which operators cannot be overloaded?
    
- Difference between member and friend overloading?
    
- Why use operator overloading?
    

---

## 21. Interview Summary

- Operator overloading = redefining operator behavior
    
- Makes objects behave like primitives
    
- Improves readability
    
- Must be used carefully
    

---

## 22. Final Mental Model

- Operator = action
    
- Overloading = teaching object how to act
    

---

Operator overloading is a powerful feature in C++ that enables **clean, expressive, and intuitive object-oriented code**, especially in domains like **math, graphics, and financial systems**.