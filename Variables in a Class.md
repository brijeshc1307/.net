##  1. Introduction

* **Variable** → A storage location used to hold a value in memory.
* In C#, inside a **class**, we can declare **4 different kinds of variables**.
* Each has its **own behavior, memory allocation rule, and life cycle**.

---

##  2. Types of Variables in a Class

| No. | Type of Variable    | Keyword Used | Also Called As        |
| --- | ------------------- | ------------ | --------------------- |
| 1   | Non-static Variable | *(none)*     | Instance Variable     |
| 2   | Static Variable     | `static`     | Class Variable        |
| 3   | Constant Variable   | `const`      | Compile-time Constant |
| 4   | Read-only Variable  | `readonly`   | Run-time Constant     |

---

##  3. Non-Static (Instance) Variables

### ➤ Definition:

* Declared **without** any modifier (`static`, `const`, etc.).
* One **separate copy** of the variable is created **for every instance** (object) of the class.

```csharp
class Program
{
    int x = 100; // non-static variable

    static void Main()
    {
        Program p1 = new Program();
        Program p2 = new Program();
    }
}
```

### ➤ Behavior:

* Memory for `x` is allocated **only after creating an object**.
* Each object has its **own copy**.
* Initialized every time a new instance is created.

### ➤ Access:

* Must be accessed using the **object reference**.

  ```csharp
  Console.WriteLine(p1.x); // ✅
  Console.WriteLine(x);    // ❌ Error
  ```

### ➤ Summary:

| Feature          | Non-Static Variable         |
| ---------------- | --------------------------- |
| Requires object? | ✅ Yes                       |
| Copies created   | One per object              |
| When initialized | At object creation          |
| Can be modified? | ✅ Yes                       |
| Lifetime         | Exists till object is alive |

---

##  4. Static Variables

### ➤ Definition:

* Declared using the **`static`** keyword.
* A **single copy** is shared across **all instances** of the class.

```csharp
class Program
{
    static int y = 200; // static variable
}
```

### ➤ Behavior:

* Memory is allocated **immediately** once the class execution begins (before any instance is created).
* Exists **for the entire life cycle of the class** (loaded once into memory).

### ➤ Access:

* Can be accessed **directly by class name** (no object required).

  ```csharp
  Console.WriteLine(Program.y);
  ```

### ➤ Summary:

| Feature          | Static Variable          |
| ---------------- | ------------------------ |
| Requires object? | ❌ No                     |
| Copies created   | One for entire class     |
| When initialized | When class is loaded     |
| Can be modified? | ✅ Yes                    |
| Lifetime         | Entire program execution |

---

##  5. Constant Variables (`const`)

### ➤ Definition:

* Declared using the **`const`** keyword.
* **Must** be initialized **at the time of declaration**.
* Value **cannot be changed** later (compile-time constant).

```csharp
const float PI = 3.14F;
```

### ➤ Important Rules:

* Must be assigned **at declaration**.
* Cannot assign later.
* Value **cannot be modified** after declaration.
* **Behaves like a static variable** (one copy per class, not per instance).
* Does **not** depend on object creation.

### ➤ Behavior:

* Memory allocated **once**, when the class starts executing.
* **No instance required** to access.

```csharp
Console.WriteLine(Program.PI); // ✅ works without object
```

### ➤ Summary:

| Feature          | Constant Variable    |
| ---------------- | -------------------- |
| Requires object? | ❌ No                 |
| Copies created   | One for entire class |
| Initialization   | At declaration       |
| Can be modified? | ❌ No                 |
| Lifetime         | Whole program        |
| Similar to       | Static variable      |

---

##  6. Read-Only Variables (`readonly`)

### ➤ Definition:

* Declared using the **`readonly`** keyword.
* Value **can be assigned either**:

  1. **At declaration**, or
  2. **Inside a constructor**.

```csharp
class Program
{
    readonly bool flag; // no initialization here

    public Program(bool f)
    {
        flag = f; // initialized in constructor
    }
}
```

### ➤ Behavior:

* **Cannot be modified after initialization** (declaration or constructor).
* Initialized **once per object**, just like instance variables.
* Each instance has its **own copy**.
* Once assigned → cannot change later.

### ➤ Example:

```csharp
class Program
{
    readonly bool flag;

    public Program(bool value)
    {
        flag = value; // initialization
    }

    static void Main()
    {
        Program p1 = new Program(true);
        Program p2 = new Program(false);

        Console.WriteLine(p1.flag); // true
        Console.WriteLine(p2.flag); // false
    }
}
```

### ➤ Summary:

| Feature                               | Read-Only Variable            |
| ------------------------------------- | ----------------------------- |
| Requires object?                      | ✅ Yes                         |
| Copies created                        | One per object                |
| Initialization                        | At declaration or constructor |
| Can be modified after initialization? | ❌ No                          |
| Lifetime                              | Same as object                |
| Similar to                            | Instance variable             |

---

##  7. Comparison Between All Four

| Feature             | Non-Static      | Static        | Constant       | Read-Only                  |
| ------------------- | --------------- | ------------- | -------------- | -------------------------- |
| Keyword             | *(none)*        | `static`      | `const`        | `readonly`                 |
| Copies per class    | One per object  | One for all   | One for all    | One per object             |
| Initialization Time | Object creation | Class loading | At declaration | Constructor or declaration |
| Can modify later?   | ✅ Yes           | ✅ Yes         | ❌ No           | ❌ No                       |
| Accessed using      | Object          | Class name    | Class name     | Object                     |
| Memory type         | Instance memory | Class memory  | Class memory   | Instance memory            |
| Requires instance?  | ✅ Yes           | ❌ No          | ❌ No           | ✅ Yes                      |
| Similar to          | —               | Constant      | Static         | Instance                   |

---

##  8. Life Cycle Summary

| Variable Type             | When Memory Allocated | How Many Times Initialized |
| ------------------------- | --------------------- | -------------------------- |
| **Static**                | When class loads      | Once per class             |
| **Instance (Non-Static)** | When object created   | Once per object            |
| **Constant**              | When class loads      | Once per class             |
| **Read-Only**             | When object created   | Once per object            |

---

##  9. Differences & Relationships

| Comparison                | Key Difference                                                                            |
| ------------------------- | ----------------------------------------------------------------------------------------- |
| **Static vs Non-Static**  | Static shared by all; non-static unique per object                                        |
| **Static vs Constant**    | Static can change; Constant cannot                                                        |
| **Constant vs Read-Only** | Constant → one copy, fixed for class; Read-Only → one copy per object, fixed per instance |
| **Instance vs Read-Only** | Instance can change; Read-Only cannot                                                     |

---

##  10. Choosing the Right Variable Type

| Requirement                      | Variable Type             |
| -------------------------------- | ------------------------- |
| Need multiple copies, modifiable | **Instance (non-static)** |
| Need single copy, modifiable     | **Static**                |
| Need single copy, fixed value    | **Constant**              |
| Need per-object fixed value      | **Read-Only**             |

---

##  **Final Summary Chart**

| Variable                  | Copies   | When Initialized   | Can Modify? | Instance Needed? | Similar To |
| ------------------------- | -------- | ------------------ | ----------- | ---------------- | ---------- |
| `int x`                   | Multiple | On object creation | ✅           | ✅                | Instance   |
| `static int y`            | One      | When class starts  | ✅           | ❌                | Class      |
| `const float PI = 3.14F;` | One      | At declaration     | ❌           | ❌                | Static     |
| `readonly bool flag;`     | Multiple | On object creation | ❌           | ✅                | Instance   |

---

###  Quick Memory Trick

| Copy Type       | Modifiable     | Variable Type |
| --------------- | -------------- | ------------- |
| Single copy     | Modifiable     | `static`      |
| Single copy     | Not modifiable | `const`       |
| Multiple copies | Modifiable     | `non-static`  |
| Multiple copies | Not modifiable | `readonly`    |

---

##  Conclusion

* All four variable types serve different **scenarios**.
* Choose based on:

  * Whether you need **single or multiple copies**.
  * Whether the value should be **modifiable or constant**.
* Summary:

  ```
  static   → single, modifiable
  const    → single, fixed
  instance → multiple, modifiable
  readonly → multiple, fixed
  ```

---


