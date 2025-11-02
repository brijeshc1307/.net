## 1. Access Specifiers

* **Access Specifiers** are **special types of modifiers** in C#.
* They define the **scope (accessibility or visibility)** of:

  * **Types (classes, structs, interfaces, etc.)**
  * **Members (fields, methods, properties, etc.)**
* They control **who can access** a particular class or member.

---

##  2. List of Access Specifiers in C#

| No. | Access Specifier     | Description                                                                |
| --- | -------------------- | -------------------------------------------------------------------------- |
| 1   | `private`            | Accessible only within the same class                                      |
| 2   | `internal`           | Accessible anywhere **within the same project**                            |
| 3   | `protected`          | Accessible **within the same class** and **child (derived) classes**       |
| 4   | `protected internal` | Accessible **within the project** *or* **child classes of other projects** |
| 5   | `public`             | Accessible **from anywhere** (no restrictions)                             |

---

##  3. Access Specifiers — Key Concept

* Access Specifiers **define visibility** — “Who can consume the member or type?”
* Example:

  * “Should this method be accessible only in this class?” → use `private`
  * “Should it be visible across the project?” → use `internal`
  * “Should child classes access it?” → use `protected`
  * “Should it be globally visible?” → use `public`

---

##  4. Access Specifiers for Members vs Classes

| Context                | Allowed Specifiers                                                         |
| ---------------------- | -------------------------------------------------------------------------- |
| **Members of a class** | All 5 (`private`, `internal`, `protected`, `protected internal`, `public`) |
| **Classes (types)**    | Only 2 → `internal` (default) and `public`                                 |

**You cannot declare a class as:** `private`, `protected`, or `protected internal`.

---

##  5. Default Scopes

| Element                | Default Specifier |
| ---------------------- | ----------------- |
| **Class**              | `internal`        |
| **Members of a class** | `private`         |

---

##  6. Access Specifier Rules Summary

| Specifier              | Accessible Within Same Class | Child Class (Same Project) | Non-Child Class (Same Project) | Child Class (Different Project) | Non-Child Class (Different Project) |
| ---------------------- | ---------------------------- | -------------------------- | ------------------------------ | ------------------------------- | ----------------------------------- |
| **private**            | ✅ Yes                        | ❌ No                       | ❌ No                           | ❌ No                            | ❌ No                                |
| **protected**          | ✅ Yes                        | ✅ Yes                      | ❌ No                           | ✅ Yes                           | ❌ No                                |
| **internal**           | ✅ Yes                        | ✅ Yes                      | ✅ Yes                          | ❌ No                            | ❌ No                                |
| **protected internal** | ✅ Yes                        | ✅ Yes                      | ✅ Yes                          | ✅ Yes                           | ❌ No                                |
| **public**             | ✅ Yes                        | ✅ Yes                      | ✅ Yes                          | ✅ Yes                           | ✅ Yes                               |

---

##  7. Practical Demonstration (Step-by-Step)

###  Class: `Program.cs`

```csharp
public class Program
{
    private void Test1() { Console.WriteLine("Private Method"); }
    internal void Test2() { Console.WriteLine("Internal Method"); }
    protected void Test3() { Console.WriteLine("Protected Method"); }
    protected internal void Test4() { Console.WriteLine("Protected Internal Method"); }
    public void Test5() { Console.WriteLine("Public Method"); }

    static void Main()
    {
        Program p = new Program();
        p.Test1();
        p.Test2();
        p.Test3();
        p.Test4();
        p.Test5();
    }
}
```

 **All methods are accessible within the same class.**

---

###  Case 1: Access from **Same Class**

➡ **All 5 methods are accessible.**

| Access             | Result       |
| ------------------ | ------------ |
| private            | ✅ Accessible |
| internal           | ✅ Accessible |
| protected          | ✅ Accessible |
| protected internal | ✅ Accessible |
| public             | ✅ Accessible |

---

###  Case 2: Access from **Child Class in Same Project**

```csharp
class Two : Program
{
    static void Main()
    {
        Two t = new Two();
        t.Test2(); // internal ✅
        t.Test3(); // protected ✅
        t.Test4(); // protected internal ✅
        t.Test5(); // public ✅
        // t.Test1(); // private ❌
    }
}
```

➡ **All except private are accessible.**

---

###  Case 3: Access from **Non-Child Class in Same Project**

```csharp
class Three
{
    static void Main()
    {
        Program p = new Program();
        p.Test2(); // internal ✅
        p.Test4(); // protected internal ✅
        p.Test5(); // public ✅
        // p.Test1(); // private ❌
        // p.Test3(); // protected ❌
    }
}
```

➡ **Accessible:** internal, protected internal, public
 Not accessible: private, protected

---

###  Case 4: Access from **Child Class in a Different Project**

Steps:

1. Create another project (e.g., `AccessDemo2`).
2. Add a reference to the first project (`AccessDemo1`).
3. Inherit the class `Program`.

```csharp
using AccessDemo1;

class Four : Program
{
    static void Main()
    {
        Four f = new Four();
        f.Test3(); // protected ✅
        f.Test4(); // protected internal ✅
        f.Test5(); // public ✅
        // f.Test1(); // private ❌
        // f.Test2(); // internal ❌
    }
}
```

➡ **Accessible:** protected, protected internal, public
❌ Not accessible: private, internal

---

###  Case 5: Access from **Non-Child Class in a Different Project**

```csharp
using AccessDemo1;

class Five
{
    static void Main()
    {
        Program p = new Program();
        p.Test5(); // public ✅
        // All others ❌
    }
}
```

➡ **Only public** is accessible.

---

##  8. Quick Summary Table (All Cases)

| Case  | Scenario                            | Accessible Members                          |
| ----- | ----------------------------------- | ------------------------------------------- |
| **1** | Same Class                          | All 5                                       |
| **2** | Child Class (Same Project)          | All except `private`                        |
| **3** | Non-Child Class (Same Project)      | `internal`, `protected internal`, `public`  |
| **4** | Child Class (Different Project)     | `protected`, `protected internal`, `public` |
| **5** | Non-Child Class (Different Project) | Only `public`                               |

---

##  9. Protected Internal Simplified

* It is a **combination of `protected` + `internal`**.
* Accessible if **either protected OR internal** is accessible.

 Boolean Logic:

```
protected_internal = protected || internal
```

| Protected | Internal | Protected Internal |
| --------- | -------- | ------------------ |
| ✅         | ✅        | ✅                  |
| ✅         | ❌        | ✅                  |
| ❌         | ✅        | ✅                  |
| ❌         | ❌        | ❌                  |

---

##  10. Important Rules

1. **Private** members → accessible only within the class.
2. **Protected** members → accessible within class + derived classes.
3. **Internal** → accessible anywhere inside the same project.
4. **Protected Internal** → accessible within same project OR from child class in another project.
5. **Public** → accessible globally (no restriction).
6. **Default for classes** → `internal`.
7. **Default for members** → `private`.
8. **Classes cannot be** `private`, `protected`, or `protected internal`.

---

##  **Final Summary**

| Specifier              | Scope                                      | Example                  |
| ---------------------- | ------------------------------------------ | ------------------------ |
| **private**            | Within same class only                     | Internal data hiding     |
| **protected**          | Same + Derived classes                     | Inheritance access       |
| **internal**           | Whole project                              | Project-level visibility |
| **protected internal** | Same project OR derived in another project | Hybrid visibility        |
| **public**             | Anywhere                                   | Global access            |

---
