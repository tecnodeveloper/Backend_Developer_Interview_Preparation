# Exception Handling in C++
---

## 1. Definition

**Exception handling** in C++ is a mechanism to handle **runtime errors** (unexpected situations) in a controlled way, preventing program crashes.

> It allows you to separate **error-handling code** from normal logic.

---

## 2. Why Exception Handling Exists

Without exception handling:

- Program may crash abruptly
- Error handling code becomes messy and scattered
- Debugging becomes difficult

With exception handling:

- Errors are handled **gracefully**
- Code becomes **clean and maintainable**
- Improves **program reliability**

---

## 3. Mental Model

Think of exception handling like a **safety net**:

- Code runs normally
- If something goes wrong → control jumps to handler
- Program recovers instead of crashing

---

## 4. Core Syntax (Concept in JS Style)

```javascript
try {
  // risky code
} catch (error) {
  // handle error
} finally {
  // always runs (optional)
}
```

---

## 5. C++ Equivalent Keywords

- `try` → block of code to monitor
- `throw` → signal an error
- `catch` → handle the error

---

## 6. Basic Example

```javascript
try {
  let result = 10 / 0;

  if (result === Infinity) {
    throw "Division by zero error";
  }

  console.log(result);
} catch (err) {
  console.log("Error:", err);
}
```

---

## 7. Step-by-Step Execution

1. Code enters `try` block    
2. Error condition detected
3. `throw` is executed
4. Control jumps to `catch`
5. Error is handled

---

## 10. Real-World Example (Backend API)

```javascript
function fetchUser(id) {
  if (!id) {
    throw "Invalid user ID";
  }
  return { id: id, name: "Ali" };
}

try {
  let user = fetchUser(null);
} catch (err) {
  console.log("API Error:", err);
}
```

---

## 11. Real-World Example (File Handling Simulation)

```javascript
function readFile(file) {
  if (!file) {
    throw "File not found";
  }
  return "File content";
}

try {
  readFile(null);
} catch (e) {
  console.log(e);
}
```

---

## 12. Internal Behavior (C++ Insight)

When an exception occurs:

```text
1. throw is executed
2. Stack unwinding begins
3. Objects are destroyed (destructors called)
4. Matching catch block is found
5. Control transferred to catch
```

---

## 13. Advanced Insight

- Exceptions propagate up the call stack
- If no handler found → program terminates
- Destructors are called automatically (RAII works)

---

## 14. Common Mistakes

---

###  Catching everything blindly

```javascript
catch (e) {
  console.log("Error");
}
```

 Fix:  
Handle specific errors properly

---

###  Not using throw properly

```javascript
throw;
```

 Fix:  
Provide meaningful message

---

###  Ignoring exceptions

```javascript
try {
  risky();
} catch (e) {}
```

 Fix:  
Always log or handle

---

## 15. Edge Cases

- Nested try-catch blocks
- Multiple catch handlers
- Exceptions in constructors/destructors
- Re-throwing exceptions

---

## 16. Multiple Catch Example

```javascript
try {
  throw "Some error";
} catch (e) {
  console.log("Handled:", e);
}
```

---

## 17. Key Points

- `try` → risky code
- `throw` → generate error
- `catch` → handle error
- Prevents crashes
- Improves code structure

---

## 18. Comparison: Exceptions vs Error Codes

|Feature|Exceptions|Error Codes|
|---|---|---|
|Readability|High|Low|
|Flow control|Automatic|Manual|
|Error handling|Centralized|Scattered|

---

## 19. Real-World Use Cases

---

### 1. Backend Systems

- API validation errors
- Database failures
- Authentication errors

---

### 2. File Handling

- File not found
- Permission denied
- Disk issues

---

## 20. Common Pitfalls

- Throwing non-standard types (like strings)
- Overusing exceptions for normal flow
- Not cleaning resources (if not using RAII)

---

## 21. Interview Tips

---

### What Interviewers Expect:

- Understanding of `try`, `catch`, `throw`
- Stack unwinding concept
- Difference between exceptions and errors
- Real-world usage

---

### Common Questions:

- What is exception handling?
- What happens when exception is thrown?
- What is stack unwinding?
- Can constructors throw exceptions?

---

## 22. Interview Summary

- Exception handling manages runtime errors
- Uses `try`, `throw`, `catch`
- Prevents crashes and improves reliability
- Works with RAII for automatic cleanup

---

## 23. Final Mental Model

- `try` → “attempt this”
- `throw` → “something went wrong”
- `catch` → “handle the problem”