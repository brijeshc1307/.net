###  1. Inheritance

**Inheritance** is a mechanism of **consuming the members (methods, variables, etc.) of one class in another class** by establishing a **parent–child (base–derived)** relationship between the classes.

> **Purpose:** To achieve **code reusability** and **avoid rewriting code**.

---

###  2. Real-Life Analogy

* A child inherits properties from parents.
* Similarly, a **child class** inherits the **members** of a **parent class**.
* Exception: **Private members** of the parent are *not inherited*.

---

###  3. Syntax

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

###  4. Advantages of Inheritance

1. **Code Reusability** – Avoids rewriting existing logic.
2. **Reduced Application Size** – No redundant code.
3. **Improved Maintainability** – Changes in base class reflect in all derived classes.

---

###  5. Example

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

###  6. Key Rules & Concepts

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

###  7. Constructor Call Chain

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

###  8. Important Notes

* Default constructor scope is **private**, so always ensure it’s **public** if you want inheritance.
* Private members are **not inherited**.
* Constructors are **not inherited**, but **called** implicitly during object creation.
* Inheritance establishes an **"is-a" relationship** (e.g., `Car` is a `Vehicle`).
* You can use **multiple levels** (multilevel inheritance), but **C# doesn’t support multiple inheritance of classes** (use interfaces for that).

---

###  9. Summary Table

| Concept              | Child → Parent             | Parent → Child             |
| -------------------- | -------------------------- | -------------------------- |
| Access to Members    | ✅ Yes (except private)     | ❌ No                       |
| Constructor Call     | Implicitly calls parent    | Not possible               |
| Reusability          | ✅ Achieved                 | ❌ N/A                      |
| Reference Conversion | `Parent p = new Child()` ✅ | `Child c = new Parent()` ❌ |

---

###  10. Debugging Tip

Use **breakpoints** and **F10 (Step Over)** / **F11 (Step Into)** in Visual Studio to trace constructor and method execution order.

---

###  **Summary**

* Inheritance enables **reusing members of an existing class**.
* Syntax: `class Derived : Base { }`
* Provides **code reusability** and **better maintainability**.
* **Child can access parent**, but **parent cannot access child**.
* **Parent constructor must be accessible** for inheritance to work.

---


## **Six Important Points of Inheritance**

### **1️⃣ Parent Class Constructor Accessibility**

* The **parent class constructor must be accessible** to the child class; otherwise, inheritance is not possible.
* When a child class object is created, the **child constructor implicitly calls the parent constructor** to initialize parent variables before using them in the child class.
* **Reason:** To ensure parent data members are properly initialized.

---

### **2️⃣ Access Rules**

* **Child classes can access parent class members**, but
* **Parent classes cannot access child class members**.
* Analogy: Children can inherit from parents, but parents cannot inherit from children.

---

### **3️⃣ Parent Reference and Child Object**

* A **parent class reference** can hold the **child class instance**, and both share the same memory.
* However, using the parent reference, **we can only access parent class members**, not child-specific members.
* Example:

  ```csharp
  Parent p = new Child();
  // p can access only Parent class members
  ```

---

### **4️⃣ Default Parent Class**

* Every class (user-defined or predefined) **inherits from the `Object` class** in the **System namespace** by default.

* Even if you don’t explicitly inherit from another class, the compiler automatically makes your class a child of `System.Object`.

* **Hierarchy Example:**

  ```
  Object → Class1 → Class2 → Class3
  ```

* **Important methods from Object class:**

  1. `Equals()`
  2. `GetHashCode()`
  3. `GetType()`
  4. `ToString()`

  These four methods are inherited by all classes in .NET.

* **Example:**

  ```csharp
  Object obj = new Object();
  Console.WriteLine(obj.GetType());
  ```

* **`GetType()`** returns the fully qualified name (Namespace + Class Name) of the object.

---

### **5️⃣ Types of Inheritance**

Inheritance can be classified based on the **number of parent and child classes**.

#### **According to C++ (theoretical classification):**

1. **Single Inheritance** – One parent, one child.
2. **Multi-level Inheritance** – Parent → Child → Grandchild chain.
3. **Hierarchical Inheritance** – One parent, multiple children.
4. **Hybrid Inheritance** – Combination of hierarchical and multi-level.
5. **Multiple Inheritance** – One child, multiple parents.

#### **Simplified View (Practical in C#):**

* **Single Inheritance:** One immediate parent class.
* **Multiple Inheritance:** More than one immediate parent class.

#### **C# Support:**

* **Supported:** Single, Multi-level, Hierarchical (one immediate parent).
* **Not Supported:** Multiple and Hybrid (more than one parent).

> **Rule:**
> In C#, only **single inheritance through classes** is supported.
> Multiple inheritance can be achieved using **interfaces**, not classes.

---

### **6️⃣ Constructor Calling Mechanism**

* When creating a child class object:

  * The **child constructor calls the parent constructor** implicitly.
  * Example call sequence:

    ```
    Object constructor → Parent constructor → Child constructor
    ```

* **If parent constructor is parameterless**, implicit calling works fine.

* **If parent constructor is parameterized**, implicit calling fails because the compiler doesn’t know which arguments to pass.

  * This causes an **error in the child class constructor**.

#### **Solution – Explicit Constructor Call**

* Use the **`base` keyword** to explicitly call the parent class constructor and pass arguments.

  ```csharp
  class Parent
  {
      public Parent(int i) { Console.WriteLine(i); }
  }

  class Child : Parent
  {
      public Child(int a) : base(a)   // Explicit call
      {
          Console.WriteLine("Child constructor");
      }
  }
  ```

* The value passed to the child constructor can be forwarded to the parent using `base()`.

* **Dynamic example:**

  ```csharp
  Child c = new Child(50);
  // Passes 50 to Child → Parent constructor
  ```

> **Rule 6 Summary:**
>
> * Implicit call works only for parameterless parent constructors.
> * For parameterized constructors, **explicit call with `base()`** is required.

---

## **Summary Table**

| Rule No. | Concept                          | Key Point                                                  |
| -------- | -------------------------------- | ---------------------------------------------------------- |
| 1        | Parent constructor accessibility | Must be accessible for inheritance                         |
| 2        | Member access                    | Child → Parent (yes), Parent → Child (no)                  |
| 3        | Reference behavior               | Parent ref → Child object (can’t access child members)     |
| 4        | Default parent                   | All classes inherit from `System.Object`                   |
| 5        | Types of inheritance             | C# supports only single inheritance through classes        |
| 6        | Constructor chaining             | Implicit for parameterless; use `base()` for parameterized |

---

# **Using Inheritance in Application Development**

### **Introduction**

* Inheritance is a key **Object-Oriented Programming (OOP)** concept that allows one class (child/derived class) to reuse properties and methods of another class (parent/base class).
* Inheritance is not something added in the middle of a project; it’s typically **planned at the initial stage of application design**.
* The main purpose is to achieve **code reusability** and **hierarchical organization** of entities in an application.

---

## **Concept of Entities**

### **What is an Entity?**

* In **DBMS terminology**, an **entity** is a living or non-living object associated with a **set of attributes**.
* Applications are built around **entities**, each representing something meaningful within the application’s domain.

### **Examples of Entities**

| Application       | Entity   |
| ----------------- | -------- |
| Banking System    | Customer |
| School Management | Student  |
| Business/Company  | Employee |

Entities can be **living (students, employees)** or **non-living (phones, pens)**—as long as they have attributes.

---

## **Examples of Attributes**

| Entity                 | Attributes                                                  |
| ---------------------- | ----------------------------------------------------------- |
| **Phone (non-living)** | Company, Model, Price, Weight, Size, Screen width, Features |
| **Pen (non-living)**   | Color, Length, Diameter, Price, Manufacturer                |
| **Student (living)**   | ID, Name, Address, Phone, Class, Marks, Grade, Fees         |
| **Employee (living)**  | EmpNo, Name, Job, Salary, DeptNo, DeptName                  |
| **Customer**           | CustomerID, Name, Address, Phone, AccountType, Balance      |

---

## **Steps to Apply Inheritance in Application Development**

### **🔹 Step 1: Identify Entities**

Identify all entities associated with the application.
**Example – School Application:**

1. Student
2. Teaching Staff
3. Non-Teaching Staff

---

### **🔹 Step 2: Identify Attributes of Each Entity**

Define what data (attributes) each entity should have.

#### **Student**

* ID
* Name
* Address
* Phone
* Class
* Marks
* Grade
* Fees

#### **Teaching Staff**

* ID
* Name
* Address
* Phone
* Designation
* Salary
* Qualification
* Subject

#### **Non-Teaching Staff**

* ID
* Name
* Address
* Phone
* Designation
* Salary
* Department Name
* Manager ID

---

### **🔹 Step 3: Identify Common Attributes and Arrange Hierarchically**

* Many entities share common attributes (**ID, Name, Address, Phone**).
* If we define all three classes separately, these attributes will repeat — leading to **code duplication**.
* To **eliminate redundancy**, identify the **common attributes** and place them in a **parent class**.

#### **Common Attributes**

* ID
* Name
* Address
* Phone

#### **Hierarchy Planning**

* **Person** → common base for all (holds ID, Name, Address, Phone)
* **Student** → inherits from **Person**
* **Staff** → inherits from **Person**

  * **Teaching Staff** → inherits from **Staff**
  * **Non-Teaching Staff** → inherits from **Staff**

This hierarchy ensures **maximum code reusability** and logical grouping.

---

### **🔹 Step 4: Define the Classes (Implementation)**

#### **Class 1: Person**

Contains all common attributes.

```csharp
public class Person
{
    public int ID;
    public string Name;
    public string Address;
    public string Phone;
}
```

#### **Class 2: Student (inherits Person)**

Adds student-specific attributes.

```csharp
public class Student : Person
{
    public string ClassName;
    public float Marks;
    public string Grade;
    public double Fees;
}
```

#### **Class 3: Staff (inherits Person)**

Adds attributes common to all staff members.

```csharp
public class Staff : Person
{
    public string Designation;
    public double Salary;
}
```

#### **Class 4: Teaching (inherits Staff)**

Adds attributes specific to teaching staff.

```csharp
public class Teaching : Staff
{
    public string Qualification;
    public string Subject;
}
```

#### **Class 5: NonTeaching (inherits Staff)**

Adds attributes specific to non-teaching staff.

```csharp
public class NonTeaching : Staff
{
    public string DepartmentName;
    public int ManagerID;
}
```

---

## **Example of Hierarchy**

```
          Person
             |
     -----------------
     |               |
  Student          Staff
                    |
          ---------------------
          |                   |
      Teaching           NonTeaching
```

---

## **Additional Example: Temporary Staff**

If a **temporary staff** category is added later:

* It shares `ID, Name, Address, Phone` (so inherits from `Person`)
* Has different attributes like **Wage** instead of Salary.

```csharp
public class TemporaryStaff : Person
{
    public double Wage;
}
```

---

## **Summary of Steps**

| Step  | Description                                            | Example                                     |
| ----- | ------------------------------------------------------ | ------------------------------------------- |
| **1** | Identify entities                                      | Student, Teaching Staff, Non-Teaching Staff |
| **2** | Identify attributes for each                           | ID, Name, etc.                              |
| **3** | Identify and organize common attributes hierarchically | Common → Person                             |
| **4** | Define classes based on hierarchy                      | Person → Staff → Teaching/NonTeaching       |

---

## **Key Takeaways**

* **Entities** represent real-world objects used in applications.
* **Attributes** are properties that describe each entity.
* **Classes** represent entities in **OOP** (like tables in DBMS or structures in procedural languages).
* **Inheritance** helps eliminate **code duplication** and improves **reusability**.
* Always plan your **class hierarchy** at the **beginning of application development**.
* **Structures** in procedural programming do not support inheritance, whereas **classes** in OOP do.

---

---
[⬅️ Constructors](/Construcor.md)      |  [ Encapsulations And Abstraction ➡️](/Encapsulations_Abstraction.md)
---

