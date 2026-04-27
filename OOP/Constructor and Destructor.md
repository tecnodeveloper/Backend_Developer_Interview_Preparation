# Constructor and Destructor

---

## 1. Definition

- A **constructor** is a special member function that is automatically called when an object is created. It initializes the object.

- A **destructor** is a special function that is automatically called when an object is destroyed. It cleans up resources.
---

## 2. Why Constructors and Destructors Exist

Without them:

- Objects may start in an **uninitialized state**
- Memory/resources may **leak**

With them:

- Constructors ensure **proper initialization**
- Destructors ensure **automatic cleanup**
- Enable **RAII (Resource Acquisition Is Initialization)**

---

## 3. Mental Model

Think of an object like a **hotel room**:
- Constructor → preparing the room before guest arrives
- Destructor → cleaning the room after guest leaves

---

## 4. Syntax

```cpp
#include <iostream>
using namespace std;

class Example {
public:
    int value;

    // Constructor
    Example(int v) {
        value = v;
        cout << "Constructor called\n";
    }

    // Destructor
    ~Example() {
        cout << "Destructor called\n";
    }
};
```

---
##  Example

```cpp
#include <iostream>
using namespace std;

class User {
public:
    string name;
    int age;

    User(string n, int a) {
        name = n;
        age = a;
    }
};

int main() {
    User user1("Ali", 25);
    cout << user1.name << endl; // Ali
}
```

---

## 6. Step-by-Step Execution

1. `User user1("Ali", 25);` is called
2. Memory is allocated
3. Constructor runs automatically
4. Values assigned
5. Object is ready


---

## 7. Intermediate Example (Default Values)

```cpp
#include <iostream>
using namespace std;

class Product {
public:
    string name;
    int price;

    Product(string n, int p = 0) {
        name = n;
        price = p;
    }
};

int main() {
    Product item("Book");
    cout << item.price << endl; // 0
}
```

---

## 8. Real-World Example (Database Connection)

```cpp
#include <iostream>
using namespace std;

class DatabaseConnection {
public:
    string connectionString;

    DatabaseConnection(string conn) {
        connectionString = conn;
        cout << "Connected to DB\n";
    }

    ~DatabaseConnection() {
        cout << "Disconnected from DB\n";
    }
};

int main() {
    DatabaseConnection db("localhost");
}
```

---

## 9. Incorrect Example

```cpp
class User {
public:
    string name;

    User(string name) {
        name = name; //  wrong
    }
};
```

###  Fix

```cpp
this->name = name;
```

---

## 10. Common Mistakes

- Forgetting `this->`
- Heavy logic in constructor
- Not initializing members properly

---

## 11. Key Points

- Same name as class    
- No return type
- Called automatically 
- Can be overloaded

---

## 12. Interview Tip

Constructor = **object initialization**

---

# Destructor

---

## 13. Definition

A destructor is used to **release resources automatically** when an object is destroyed.

---

## 14. Basic Example

```cpp
#include <iostream>
using namespace std;

class FileHandler {
public:
    FileHandler() {
        cout << "File opened\n";
    }

    ~FileHandler() {
        cout << "File closed\n";
    }
};

int main() {
    FileHandler file;
}
```

---

## 15. Step-by-Step Execution

1. Object created → constructor runs
2. Program ends or scope ends
3. Destructor runs automatically
4. Resources cleaned

---

## 16. Real-World Example

```cpp
#include <iostream>
using namespace std;

class Array {
private:
    int* arr;

public:
    Array(int size) {
        arr = new int[size];
        cout << "Memory allocated\n";
    }

    ~Array() {
        delete[] arr;
        cout << "Memory freed\n";
    }
};

int main() {
    Array a(5);
}
```

---

## 17. Incorrect Example (Memory Leak)

```cpp
class Test {
public:
    int* data;

    Test() {
        data = new int[10];
    }

    //  No destructor → memory leak
};
```

---

### Fix

```cpp
~Test() {
    delete[] data;
}
```

---

## 18. Common Mistakes

- Forgetting to free dynamic memory
- Double deletion
- Using deleted memory (dangling pointer)

---

## 19. Key Points

- Same name as class with `~`
- No parameters, no return type
- Called automatically
- Only one destructor per class

---

## 20. Interview Tip

Destructor = **automatic cleanup**

---

#  Constructor vs Destructor

|Feature|Constructor|Destructor|
|---|---|---|
|Purpose|Initialize object|Clean resources|
|Execution|On creation|On destruction|
|Name|Class name|~ClassName|
|Parameters|Allowed|Not allowed|
|Overloading|Yes|No|

---

#  Edge Cases & Pitfalls

- Memory leaks if destructor missing
- Dangling pointers after deletion
- Order of destruction (reverse order of creation)
- Exceptions in constructor can prevent full initialization

---
## 1. Backend System (Resource Management)

```cpp
class APIClient {
public:
    APIClient() {
        cout << "Client initialized\n";
    }

    ~APIClient() {
        cout << "Client destroyed\n";
    }
};
```

---

## 2. File Handling System

```cpp
#include <fstream>

class FileManager {
private:
    ofstream file;

public:
    FileManager() {
        file.open("data.txt");
    }

    ~FileManager() {
        file.close();
    }
};
```

---

#  Internal Behavior (Advanced Insight)

### Constructor Internals

- Allocates memory    
- Initializes members
- Binds object

### Destructor Internals

- Called automatically when:
    - Object goes out of scope
    - `delete` is used
    
- Frees resources
- Executes in **reverse order**

---

#  Final Mental Model

- Constructor → **Setup phase**
- Destructor → **Cleanup phase**
- Together → **Lifecycle control (RAII)**

---

#  Interview Summary

- Constructor initializes object automatically
- Destructor cleans resources automatically
- Always manage dynamic memory properly
