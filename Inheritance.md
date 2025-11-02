
## 🧠 **Inheritance in C# – Notes**

### 🔹 1. Definition

**Inheritance** is a mechanism of **consuming the members (methods, variables, etc.) of one class in another class** by establishing a **parent–child (base–derived)** relationship between the classes.

> **Purpose:** To achieve **code reusability** and **avoid rewriting code**.

---

### 🔹 2. Real-Life Analogy

* A child inherits properties from parents.
* Similarly, a **child class** inherits the **members** of a **parent class**.
* Exception: **Private members** of the parent are *not inherited*.

---

### 🔹 3. Syntax

```csharp
class ChildClass : ParentClass
{
    // child-specific members
}
```

**Terminology:**

| Term         | Alternate Names           |
| ------------ | ------------------------- |
| Parent Class | Base Class / Super Class  |
| Child Class  | Derived Class / Sub Class |

---

### 🔹 4. Advantages of Inheritance

1. **Code Reusability** – Avoids rewriting existing logic.
2. **Reduced Application Size** – No redundant code.
3. **Improved Maintainability** – Changes in base class reflect in all derived classes.

---

### 🔹 5. Example

```csharp
class Class1
{
    public void Test1() => Console.WriteLine("Method 1");
    public void Test2() => Console.WriteLine("Method 2");
}

class Class2 : Class1
{
    public void Test3() => Console.WriteLine("Method 3");
}

class Program
{
    static void Main()
    {
        Class2 c = new Class2();
        c.Test1();   // from Class1
        c.Test2();   // from Class1
        c.Test3();   // from Class2
    }
}
```

**Output:**

```
Method 1
Method 2
Method 3
```

---

### 🔹 6. Key Rules & Concepts

#### **Rule 1: Parent Constructor Accessibility**

* The **parent class constructor must be accessible** to the child class.
* Otherwise, inheritance fails.

```csharp
public class Parent
{
    public Parent() => Console.WriteLine("Parent constructor");
}

public class Child : Parent
{
    public Child() => Console.WriteLine("Child constructor");
}
```

**Execution order:**
1️⃣ Parent constructor → 2️⃣ Child constructor

If parent constructor is **private**, the compiler throws:

> *“Inaccessible due to its protection level.”*

**Reason:**
Parent must initialize its members first so the child can consume them.

---

#### **Rule 2: One-Way Access**

* **Child class** can access **parent class members**.
* **Parent class** **cannot** access members defined **only in the child class**.

```csharp
Class1 p = new Class1();
p.Test1();  // OK
p.Test3();  // ❌ Error – Parent cannot access child members
```

---

#### **Rule 3: Parent Reference Using Child Instance**

You can assign a **child class object** to a **parent class reference**.

```csharp
Class2 c = new Class2();
Class1 p = c;   // Parent reference → Child instance
p.Test1();      // OK
p.Test2();      // OK
p.Test3();      // ❌ Not accessible
```

✅ **Explanation:**

* `p` (parent reference) consumes the **same memory** as `c` (child instance).
* However, it can only access **members defined in the parent class**.

> “You can look **upward** (child → parent), but not **downward** (parent → child).”

---

### 🔹 7. Constructor Call Chain

When multiple classes are inherited:

```csharp
class A { public A() { Console.WriteLine("A"); } }
class B : A { public B() { Console.WriteLine("B"); } }
class C : B { public C() { Console.WriteLine("C"); } }

new C();
```

**Output:**

```
A
B
C
```

**Reason:**

* Each child constructor **implicitly calls its parent constructor**.
* Initialization starts **from the topmost parent**.

---

### 🔹 8. Important Notes

* Default constructor scope is **private**, so always ensure it’s **public** if you want inheritance.
* Private members are **not inherited**.
* Constructors are **not inherited**, but **called** implicitly during object creation.
* Inheritance establishes an **"is-a" relationship** (e.g., `Car` is a `Vehicle`).
* You can use **multiple levels** (multilevel inheritance), but **C# doesn’t support multiple inheritance of classes** (use interfaces for that).

---

### 🔹 9. Summary Table

| Concept              | Child → Parent             | Parent → Child             |
| -------------------- | -------------------------- | -------------------------- |
| Access to Members    | ✅ Yes (except private)     | ❌ No                       |
| Constructor Call     | Implicitly calls parent    | Not possible               |
| Reusability          | ✅ Achieved                 | ❌ N/A                      |
| Reference Conversion | `Parent p = new Child()` ✅ | `Child c = new Parent()` ❌ |

---

### 🔹 10. Debugging Tip

Use **breakpoints** and **F10 (Step Over)** / **F11 (Step Into)** in Visual Studio to trace constructor and method execution order.

---

### ✅ **Summary**

* Inheritance enables **reusing members of an existing class**.
* Syntax: `class Derived : Base { }`
* Provides **code reusability** and **better maintainability**.
* **Child can access parent**, but **parent cannot access child**.
* **Parent constructor must be accessible** for inheritance to work.

---

Would you like me to also make a **diagram** showing how memory/reference sharing happens between parent and child (like the one the instructor described with `p` and `c`)?
