### **1. What is a Class?**

* A **class** is a **user-defined type** in Object-Oriented Programming (OOP), similar to **structures** in C language.
* However, the main difference is:

  * A **structure (struct)** in C can contain only **variables**.
  * A **class** can contain both **variables** and **functions (methods)**.

---

### **2. Syntax to Define Class and Structure**

| **Structure (C)**                 | **Class (OOP)**                               |
| --------------------------------- | --------------------------------------------- |
| `struct <Name> { <variables>; };` | `class <Name> { <variables>; <functions>; };` |

**Example:**

```cpp
struct Student
{
    int Id;
    char Name[25];
    float Marks, Fees;
};

class Employee
{
    int Id;
    string Name, Job;
    float Salary;
    // Can also have functions
};
```

---

### **3. Predefined and User-Defined Types**

* **Predefined types**: `int`, `float`, `char`, `string`
* **User-defined types**: `Student`, `Employee`

**Difference:**

* Predefined types are **scalar** types → can hold **only one value**.
* User-defined types are **complex** types → can hold **multiple values**.

---

### **4. Consuming a Type (Creating Copies)**

* Types themselves **cannot be used directly**, since they do **not have memory allocation**.
  Example:

  ```cpp
  int = 100; // Invalid
  int i = 100; // Valid
  ```
* You must **create a copy** (variable/object) of the type to allocate memory.

**Examples:**

```cpp
int i;           // Copy of predefined type int
string s;        // Copy of predefined type string
Student ss;      // Copy of user-defined type Student
Employee emp;    // Copy of user-defined type Employee
```

---

### **5. Variables vs Objects**

| **Type**                                      | **Copy is Called**         |
| --------------------------------------------- | -------------------------- |
| Scalar types (`int`, `float`, `string`, etc.) | **Variable**               |
| Complex types (`Student`, `Employee`, etc.)   | **Object** or **Instance** |

**Conclusion:**
After defining a class or structure, to **use (consume)** it, we must **create an object or instance**, which allocates memory. Only through that object can we access the members (variables or methods) defined inside it.

---

### **6. Object-Oriented Programming in C++**

* **C++** was the first **Object-Oriented Programming Language**.
* However, it’s **not fully Object-Oriented**, because:

  * The **main() function** is written **outside the class**.
  * OOP principles suggest that *every part of the program should be inside a class*.

#### **Reason: Circular Dependency Problem**

If `main()` were inside a class:

* It becomes a member of the class → can only be called through an object.
* But, the object is created inside `main()`.
  → **Neither can start first**, leading to a *circular dependency*.

So, in C++, the `main()` function is kept **outside the class**.

---

### **7. Object-Oriented Programming in Java**

* **Java** (introduced in 1995) also defines classes as **collections of variables and methods**.
* Java designers wanted it to be **fully Object-Oriented**, meaning even the `main()` method should be **inside the class**.

#### **Solution: Static Members**

Java divides class members into:

1. **Non-static members** – need an object to access.
2. **Static members** – can be accessed **without** an object.

**Example:**

```java
class Test {
    int x = 100;          // Non-static member
    static int y = 200;   // Static member
}
```

* The `main()` method is **static**, so it can run without needing an object:

  ```java
  public static void main(String[] args) {
      // Code here
  }
  ```

---

### **8. Object-Oriented Programming in C#**

* **C#** was introduced after Java and is heavily influenced by it.
* The `Main()` method is also **defined inside a class** and declared as **static**.
* If the class contains **only the Main() method**, we do **not need to create any object**.

---

### **9. Writing Programs in C#**

#### **Standards and Conventions**

1. **Case Sensitivity**

   * Keywords → lowercase (`class`, `static`, etc.)
   * Library names → **Pascal Case** (`WriteLine`, `ReadLine`)
   * User-defined names → **Pascal Case suggested**, though any casing works.

2. **File Extension**

   * Save C# programs with **“.cs”** extension.

3. **File Naming**

   * Suggested: **Filename = Class name**.

4. **Development Environment**

   * Preferably use **Visual Studio .NET (IDE)**.
   * Alternatively, programs can be written in **Notepad** and compiled via command line.

---

### **10. Syntax in C#**

#### **Class Definition**

```csharp
[<modifiers>] class <Name>
{
    // Members here
}
```

* **modifiers**: special keywords like `public`, `internal`, `static`, `abstract`, `partial`, `sealed`.
* **class**: keyword to define a class.
* **Name**: name of the class.
* **Members**: variables (fields) or methods.

---

#### **Main Method Syntax**

```csharp
static void Main(string[] args)
{
    // Statements
}
```

**Explanation:**

* `static`: allows execution **without** creating an object.
* `void`: indicates **no return value**.
* `Main`: name of the entry point method (should be in **Pascal Case**).
* `string[] args`: optional parameter used to pass command-line arguments.
* Statements: code logic to be executed.

---

✅ **Summary**

* Classes are user-defined types combining **data (variables)** and **behavior (functions)**.
* Objects are **instances** of classes with allocated memory.
* **C++**: Not fully OOP (main outside class).
* **Java & C#**: Fully OOP (main inside class, declared static).
* **C#** follows strict naming, syntax, and structure rules for clarity and consistency.

---

---
[⬅️ Basics](/cs_basics.md)      |          [Costructor ➡️](/construcor.md)
---
