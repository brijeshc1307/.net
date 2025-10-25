
---

## 🔹 1. What is a Constructor?

* A **Constructor** is a **special method** present inside a **class**.
* It is **responsible for initializing the variables (fields)** of that class.
* It is automatically called **when an object of the class is created**.
* Every class **must have a Constructor** (either defined by the programmer or automatically added by the compiler).

---

## 🔹 2. Characteristics of a Constructor

1. **Same name as the class**

   * The name of the Constructor **must exactly match** the name of the class.
   * Example:

     ```csharp
     class Test {
         public Test() {
             // Constructor body
         }
     }
     ```
   * If class name is `Test`, Constructor name must be `Test`.

2. **No return type**

   * Constructors **do not return any value** (not even `void`).
   * Hence, they are called **non-value-returning methods**.

3. **Executed automatically**

   * The Constructor runs automatically when an instance of the class is created.

4. **Used for variable initialization**

   * It initializes class variables either to **default values** or to values defined by the programmer.

---

## 🔹 3. Importance of Constructors

* Without a Constructor, you **cannot create an instance** of a class.
* Example:

  ```csharp
  Test obj = new Test(); // Constructor is called here
  ```

---

## 🔹 4. Implicit (Default) Constructor

### ➤ What happens if you don’t define a Constructor?

* If the programmer **does not define** a Constructor,
  the **compiler automatically adds** one.
* This is called an **implicit Constructor** (or **default Constructor**).

### ➤ Example:

```csharp
class Test {
    int i;
    string s;
    bool b;
}
```

Even though no Constructor is defined, the compiler internally creates:

```csharp
public Test() {
    i = 0;
    s = null;
    b = false;
}
```

This means:

* All numeric variables → initialized to **0**
* Boolean variables → initialized to **false**
* String and object variables → initialized to **null**

### ➤ Points about Implicit Constructors:

1. Implicit Constructors are **parameterless** (no arguments).
2. They are also called **default Constructors**.
3. They are always **public** by default.
4. Every class you’ve ever created (even without defining one) already had a default Constructor defined by the compiler.

---

## 🔹 5. Explicit Constructor

### ➤ Definition

* When the programmer **manually defines** a Constructor inside a class,
  it is called an **explicit Constructor**.

### ➤ Syntax:

```csharp
[modifier] ClassName([parameters]) {
    // statements
}
```

Example:

```csharp
public class ExplicitConDemo {
    public ExplicitConDemo() {
        Console.WriteLine("Constructor is called");
    }
}
```

### ➤ Usage:

```csharp
ExplicitConDemo obj = new ExplicitConDemo();
```

Output:

```
Constructor is called
```

Every time you create an object, the Constructor executes.

### ➤ Example with multiple instances:

```csharp
ExplicitConDemo obj1 = new ExplicitConDemo();
ExplicitConDemo obj2 = new ExplicitConDemo();
ExplicitConDemo obj3 = new ExplicitConDemo();
```

Output:

```
Constructor is called
Constructor is called
Constructor is called
```

> ✔ Each time an object is created, the Constructor is called once.

---

## 🔹 6. Types of Constructor Definitions

| Type                     | Who Defines It | Parameters                            | Access Modifier | Other Name               |
| ------------------------ | -------------- | ------------------------------------- | --------------- | ------------------------ |
| **Implicit Constructor** | Compiler       | None (parameterless)                  | Public          | Default Constructor      |
| **Explicit Constructor** | Programmer     | Can be parameterless or parameterized | Defined by user | User-defined Constructor |

---

## 🔹 7. Constructor Call (Execution)

### ➤ Important Concepts:

* **Defining a Constructor** means writing the Constructor code inside a class.

  * It can be **implicit** (by compiler) or **explicit** (by programmer).
* **Calling a Constructor** happens when we create an object using `new`.

  * Example:

    ```csharp
    Test obj = new Test(); // This explicitly calls the Constructor
    ```
* **Calling is always explicit** — it happens when you use the `new` keyword.

  * Even though the Constructor may be implicit, the call to it is explicit.

---

## 🔹 8. Step-by-Step Example

### Example 1 — Implicit Constructor

```csharp
class Program {
    int i;
    bool b;
    
    static void Main() {
        Program p = new Program();
        Console.WriteLine("Value of i is " + p.i);
        Console.WriteLine("Value of b is " + p.b);
    }
}
```

**Output:**

```
Value of i is 0
Value of b is False
```

**Explanation:**
The values come from the **implicit (default) Constructor** created by the compiler.

---

### Example 2 — Explicit Constructor

```csharp
class ExplicitConDemo {
    public ExplicitConDemo() {
        Console.WriteLine("Constructor is called");
    }
    
    static void Main() {
        ExplicitConDemo obj1 = new ExplicitConDemo();
        ExplicitConDemo obj2 = new ExplicitConDemo();
    }
}
```

**Output:**

```
Constructor is called
Constructor is called
```

---

## 🔹 9. Key Points Recap

| Concept              | Explanation                                                        |
| -------------------- | ------------------------------------------------------------------ |
| Constructor          | Special method inside a class for variable initialization          |
| Name                 | Must match the class name exactly                                  |
| Return Type          | None (non-value-returning)                                         |
| Execution            | Runs automatically when object is created                          |
| Implicit Constructor | Created automatically by compiler (default, parameterless, public) |
| Explicit Constructor | Defined by the programmer (can be parameterless or parameterized)  |
| Calling              | Always explicit (through `new` keyword)                            |
| Defining             | Can be implicit or explicit                                        |
| Purpose              | Initializes class variables to default or user-defined values      |

---

## 🧩 **Constructors – Part 2 Notes**

### 🔹 **Recap from Part 1**

* **Constructor** is a **special method** in a class used to **initialize variables** of that class.
* Every class **requires a constructor** to create its **instance** (object).
* If a constructor is **not defined** by the programmer,
  the **compiler automatically defines an implicit constructor**.
* Constructors are **called explicitly** (when creating an object using `new`).

---

## ⚙️ **Types of Constructors**

There are **four types of constructors** in C#:

1. **Default (or Parameterless) Constructor**
2. **Parameterized Constructor**
3. **Copy Constructor**
4. **Static Constructor**

---

### 🟩 **1. Default / Parameterless Constructor**

* A constructor **that takes no parameters**.
* If no constructor is defined in a class, the **compiler provides one automatically** (implicit).
* Implicit constructors are:

  * Always **public**.
  * Always **parameterless**.
  * Initialize fields with **default values**:

    | Type               | Default Value |
    | ------------------ | ------------- |
    | int, float, double | 0             |
    | bool               | false         |
    | string, object     | null          |

**Example:**

```csharp
class Test
{
    // Implicit constructor: public Test() {}
}
```

If you define your own constructor, the compiler **won’t create** the implicit one.

---

### 🟨 **2. Parameterized Constructor**

* A constructor **with parameters**.
* Used to **initialize objects with specific values**.
* **Must be explicitly defined** by the programmer (no implicit parameterized constructors).

**Example:**

```csharp
class ParameterizedDemo
{
    int x;
    public ParameterizedDemo(int a)
    {
        x = a;
        Console.WriteLine("Parameterized constructor called, x = " + x);
    }

    public void Display()
    {
        Console.WriteLine("Value of x: " + x);
    }
}

class Program
{
    static void Main()
    {
        ParameterizedDemo cd1 = new ParameterizedDemo(10);
        ParameterizedDemo cd2 = new ParameterizedDemo(20);
        cd1.Display();  // x = 10
        cd2.Display();  // x = 20
    }
}
```

**Key Points:**

* Each object gets **its own copy** of the instance variables.
* Memory is allocated **separately** for each instance.
* Parameterized constructors **cannot be created implicitly**.

---

### 🟦 **3. Copy Constructor**

* Used to **create a new object as a copy of an existing object**.
* The constructor **takes the same class type as a parameter**.
* Copies the **values** from the existing object to the new one.
* Must be **explicitly defined** by the programmer.

**Example:**

```csharp
class CopyConDemo
{
    int x;

    // Normal constructor
    public CopyConDemo(int a)
    {
        x = a;
    }

    // Copy constructor
    public CopyConDemo(CopyConDemo obj)
    {
        x = obj.x;
    }

    public void Display()
    {
        Console.WriteLine("Value of x: " + x);
    }

    static void Main()
    {
        CopyConDemo cd1 = new CopyConDemo(10);
        CopyConDemo cd2 = new CopyConDemo(cd1); // Copy constructor
        cd1.Display();  // 10
        cd2.Display();  // 10
    }
}
```

**Key Points:**

* Both objects (`cd1` and `cd2`) have **separate memory**,
  but **same values** are copied.
* Useful when you need **multiple instances with identical data**.
* It is a **parameterized constructor** where the parameter is of the **same class type**.

---

### 🟥 **4. Static Constructor**

* Declared using the keyword **`static`**.
* Used to **initialize static variables** of a class.
* Executed **only once** per class — **before any object is created** or any static member is accessed.
* **Implicitly called** by the CLR (Common Language Runtime).
* **Cannot be parameterized** → **overloading not possible**.

**Example:**

```csharp
class StaticConDemo
{
    static StaticConDemo()
    {
        Console.WriteLine("Static constructor executed");
    }

    static void Main()
    {
        Console.WriteLine("Main method executed");
    }
}
```

**Output:**

```
Static constructor executed
Main method executed
```

**Key Points:**

1. If a class contains any **static variables**,
   an **implicit static constructor** will exist (if not defined).
2. If no static variable exists →
   static constructor must be **defined explicitly**.
3. **Implicitly called** — cannot be called manually.
4. **First block to execute** in the class (runs before `Main()` executes).
5. **Cannot take parameters → cannot be overloaded.**

---

## 🧠 **Summary of Constructor Types**

| Type                    | Parameterized       | Implicitly Defined       | Can Overload | Automatically Called | Purpose                         |
| ----------------------- | ------------------- | ------------------------ | ------------ | -------------------- | ------------------------------- |
| Default / Parameterless | ❌                   | ✅                        | ✅            | ✅                    | Initialize with default values  |
| Parameterized           | ✅                   | ❌                        | ✅            | ✅ (via `new`)        | Initialize with specific values |
| Copy Constructor        | ✅ (same class type) | ❌                        | ✅            | ✅ (via `new`)        | Copy data from another instance |
| Static Constructor      | ❌                   | ✅ (if static vars exist) | ❌            | ✅ (by CLR)           | Initialize static members       |

---

✅ **In short:**

> * Constructors are **special methods** used to initialize objects.
> * There are **4 types**: Default, Parameterized, Copy, and Static.
> * **Implicit constructors** are always **public and parameterless**.
> * **Static constructors** run **once per class**, before `Main()`.
> * **Copy constructors** are used to **duplicate object data**.

---
