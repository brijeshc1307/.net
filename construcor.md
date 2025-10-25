
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

Perfect 👍
Let’s organize your content into **well-structured notes**, add **explanations**, and also include a **C# example** that demonstrates all these points.

---

## 🧾 **Notes on Constructors in C# (.NET)**

### 🔹 1. Constructor Basics

* A **constructor** is a special method in a class that is called automatically when an **object** (instance) of that class is created.
* Its main purpose is to **initialize variables** or **prepare the object for use**.

---

### 🔹 2. Need for a Constructor

* Every class **requires a constructor** to create its object.
* If you don’t define one, the compiler **automatically provides an implicit (default) constructor**.

---

### 🔹 3. Implicit (Default) Constructor

* When no constructor is explicitly defined, C# automatically adds one with **no parameters**.
* This **default constructor** initializes:

  * **Value types** → with their default values (`int = 0`, `bool = false`, etc.)
  * **Reference types** → with `null`.

🟢 Example:

```csharp
class Student
{
    public string Name;
    public int Age;
}

// Compiler adds a default constructor automatically
```

When you create:

```csharp
Student s = new Student();
```

Both `Name` and `Age` will be initialized to default values:
`Name = null`, `Age = 0`.

---

### 🔹 4. Why Define a Constructor Explicitly?

* The **implicit constructor** always initializes variables with the **same values** every time a new instance is created.
* If you want to assign **different values** to each instance, you must define an **explicit (parameterized) constructor**.

---

### 🔹 5. Parameterized Constructor

* A constructor can take **parameters** so that different objects can be initialized with **different values** each time.
* This provides **flexibility** and **custom initialization**.

🟢 Example:

```csharp
class Student
{
    public string Name;
    public int Age;

    // Explicit constructor with parameters
    public Student(string name, int age)
    {
        Name = name;
        Age = age;
    }
}
```

Now, each instance can have different data:

```csharp
Student s1 = new Student("Alice", 20);
Student s2 = new Student("Bob", 22);
```

---

### 🔹 6. When to Define Constructors Explicitly

Whenever a class needs **specific values** to execute properly (for example, configuration data, user info, etc.),
you should define a constructor and pass values to it.

🟢 Rule of Thumb:

> “If a class requires data to work, pass that data through a constructor.”

---

### 🔹 7. Summary

| Type of Constructor | Added By  | Takes Parameters | Purpose                                  |
| ------------------- | --------- | ---------------- | ---------------------------------------- |
| Implicit (Default)  | Compiler  | No               | Initialize with default values           |
| Explicit (Default)  | Developer | No               | Initialize with specific values          |
| Parameterized       | Developer | Yes              | Initialize with custom values per object |

---

## 💡 **Example: Implicit vs Explicit Constructor**

```csharp
using System;

class Employee
{
    public string Name;
    public int Salary;

    // 1️⃣ Implicit constructor (if this one wasn’t here, compiler adds its own)
    // public Employee() { }

    // 2️⃣ Explicit parameterized constructor
    public Employee(string name, int salary)
    {
        Name = name;
        Salary = salary;
    }
}

class Program
{
    static void Main()
    {
        // Using the explicit constructor
        Employee e1 = new Employee("John", 30000);
        Employee e2 = new Employee("Mary", 40000);

        Console.WriteLine($"Employee 1: {e1.Name}, Salary: {e1.Salary}");
        Console.WriteLine($"Employee 2: {e2.Name}, Salary: {e2.Salary}");
    }
}
```

**Output:**

```
Employee 1: John, Salary: 30000
Employee 2: Mary, Salary: 40000
```

---

## ✅ **Key Takeaways**

1. Every class has a constructor — either **implicit** or **explicit**.
2. The **implicit constructor** initializes variables with **default values**.
3. The **explicit constructor** allows **custom initialization** per object.
4. Whenever your class **requires input values to function**, define a **parameterized constructor**.
5. Constructors help make your objects more **dynamic, reliable, and maintainable**.

---

Excellent — this is a full lecture transcription from **Naresh i Technologies (Bangarraju sir)** explaining the **difference between static and non-static constructors in C#**.

Here’s a **clean, structured, point-wise summary (notes)** in a professional format with **key C# concepts**, **rules**, and **examples**.

---

# 🧾 Notes: Difference Between Static and Non-Static Constructors in C#

---

## 🔹 1. What is a Constructor?

* A **constructor** is a special method in a class that initializes the fields or variables of that class.
* It is automatically invoked when an object of the class is created.
* Purpose: To **initialize the fields/variables** of the class.

---

## 🔹 2. Static vs Non-Static Constructors

| Feature                             | **Static Constructor**                                                      | **Non-Static Constructor (Instance Constructor)**                              |
| ----------------------------------- | --------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| **Declaration**                     | Declared using the `static` keyword                                         | Declared **without** `static` keyword                                          |
| **Purpose**                         | Initializes **static fields** of the class                                  | Initializes **non-static fields** of the class                                 |
| **Call Type**                       | **Implicitly** called by CLR                                                | **Explicitly** called when creating an object                                  |
| **Execution Time**                  | Executes **once**, automatically, before any object is created              | Executes **every time** an object is created                                   |
| **Execution Order**                 | Executes **first** — before the `Main()` method or any instance constructor | Executes **after** object creation                                             |
| **Parameters**                      | Cannot have parameters                                                      | Can have parameters                                                            |
| **Overloading**                     | Cannot be overloaded                                                        | Can be overloaded                                                              |
| **Implicit Definition**             | Implicitly defined **only if the class has static fields**                  | Implicitly defined in **every class except static classes**                    |
| **Access to Members**               | Can access only **static members**                                          | Can access **both static and non-static members**                              |
| **Execution Count (per lifecycle)** | Executes **only once per class**                                            | Executes **0 times** (if no instances) or **N times** (if N instances created) |

---

## 🔹 3. Key Points to Remember

1. **Static fields** → initialized by **static constructor**.
   **Non-static fields** → initialized by **non-static constructor**.

2. **Static constructor**

   * Is **implicitly called** by the runtime (CLR).
   * Cannot be **called explicitly**.
   * Cannot take **parameters**.
   * Cannot be **overloaded**.
   * Executes **once per class** before any instance or `Main()` executes.

3. **Non-static constructor**

   * Must be **explicitly called** when creating an object.
   * Can have **parameters**.
   * Can be **overloaded**.
   * Executes **each time** an object is created.

4. **Implicit Constructors**

   * Every **non-static class** automatically gets an **implicit (default) constructor** if no explicit one is defined.
   * A **static constructor** is implicitly created **only if static fields exist** in the class.
   * A **static class** cannot have a non-static constructor.

---

## 🔹 4. Execution Order Example

```csharp
using System;

class ConstructorsDemo
{
    static int y;
    int x;

    // Static constructor
    static ConstructorsDemo()
    {
        Console.WriteLine("Static constructor is called");
    }

    // Non-static constructor
    public ConstructorsDemo()
    {
        Console.WriteLine("Non-static constructor is called");
    }

    static void Main()
    {
        Console.WriteLine("Main method started");

        ConstructorsDemo d1 = new ConstructorsDemo();
        ConstructorsDemo d2 = new ConstructorsDemo();

        Console.ReadLine();
    }
}
```

**Output:**

```
Static constructor is called
Main method started
Non-static constructor is called
Non-static constructor is called
```

✅ **Explanation:**

* Static constructor executes **once**, automatically, before the first access to the class.
* Main method runs **after** the static constructor.
* Non-static constructor executes **each time** an instance is created.

---

## 🔹 5. Parameterized Constructor Example

```csharp
using System;

class ConstructorsDemo
{
    int x;
    static int y;

    // Static constructor
    static ConstructorsDemo()
    {
        y = 100;
        Console.WriteLine("Static constructor is called");
    }

    // Non-static (parameterized) constructor
    public ConstructorsDemo(int val)
    {
        x = val;
        Console.WriteLine($"Non-static constructor called with value: {x}");
    }

    static void Main()
    {
        ConstructorsDemo d1 = new ConstructorsDemo(10);
        ConstructorsDemo d2 = new ConstructorsDemo(20);
        ConstructorsDemo d3 = new ConstructorsDemo(30);
    }
}
```

**Output:**

```
Static constructor is called
Non-static constructor called with value: 10
Non-static constructor called with value: 20
Non-static constructor called with value: 30
```

✅ **Explanation:**

* Static constructor → executes once at the start.
* Non-static constructor → executes **three times** for three instances.
* Static constructor **cannot** take parameters, while non-static can.

---

## 🔹 6. Why Static Constructors Cannot Have Parameters

* Because **they are implicitly called** by CLR — the developer does **not** call them manually.
* Since you can’t call it explicitly, there’s **no way to pass arguments** to it.
* Also, static constructors run **before any code**, so **no prior data** is available to pass as parameters.

---

## 🔹 7. Why Static Constructors Cannot Be Overloaded

* Overloading is based on **different parameter lists**.
* Static constructors **cannot have parameters**, hence **overloading** is not possible.

---

## 🔹 8. Summary Table

| Concept         | Static Constructor           | Non-Static Constructor      |
| --------------- | ---------------------------- | --------------------------- |
| Keyword         | `static`                     | (No keyword)                |
| Called by       | CLR (Implicitly)             | Developer (Explicitly)      |
| Parameters      | Not allowed                  | Allowed                     |
| Overloading     | Not allowed                  | Allowed                     |
| Access Members  | Only static members          | Static + Non-static members |
| Execution Time  | Before any object is created | During object creation      |
| Execution Count | Once per class               | For every object            |
| Purpose         | Initialize static fields     | Initialize instance fields  |

---

## ✅ **Key Takeaways**

* Static constructors are for **class-level initialization**.
* Non-static constructors are for **object-level initialization**.
* Static constructors run **only once per class**, automatically.
* Non-static constructors run **every time an instance is created**.
* Static constructors **cannot** have parameters or be overloaded.
* Every class (except static classes) has an **implicit non-static constructor** if none is defined.
* Static constructors are **implicitly defined only** when static fields exist.

---

