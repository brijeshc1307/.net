
# **Method Overloading**

### **What is Method Overloading?**

**Method Overloading means** defining **multiple methods** inside the **same class** with the **same method name** but with **different parameters**.

So **method name is same**, but parameters will be **different**.
That is what we call **Overloading**.

---

### **Why Ambiguity Does Not Come?**

Because **compiler** looks at **parameter list** (also called **method signature**) to identify which method to run.

So:

* **Name is same** → allowed
* **Parameters must be different** → required

---

### **How Parameters Can Be Different?**

We can change:

1. **Number of parameters**
2. **Type of parameters**
3. **Order of parameters**

#### **Diagram**

```
              Method Overloading
                       |
       --------------------------------
       |              |               |
 Change Number   Change Type     Change Order
```

---

### **Examples**

```csharp
public void Test()                 // 1. no parameter
public void Test(int i)            // 2. number changed
public void Test(string s)         // 3. type changed
public void Test(int i, string s)  // 4. order one
public void Test(string s, int i)  // 5. order reversed
```

All these are **valid** overloads because parameters are different.

---

### **Important NOTE**

```csharp
public void Test()
public string Test()     // ❌ INVALID
```

Changing **return type only** does **NOT** count as overloading.
Because **return type is checked at the end**, but compiler must know **which method to call at start**.
If two methods have same name and same parameters → there will be **ambiguity**, so it's **not allowed**.

---

### **Simple Practical Example**

```csharp
class Program {
   public void Test() {
      Console.WriteLine("First Method");
   }

   public void Test(int i) {
      Console.WriteLine("Second Method");
   }

   public void Test(string s) {
      Console.WriteLine("Third Method");
   }

   public void Test(int i, string s) {
      Console.WriteLine("Fourth Method");
   }

   public void Test(string s, int i) {
      Console.WriteLine("Fifth Method");
   }

   static void Main() {
      Program p = new Program();
      p.Test();              // First Method
      p.Test(10);            // Second Method
      p.Test("ABC");         // Third Method
      p.Test(10, "ABC");     // Fourth Method
      p.Test("ABC", 10);     // Fifth Method
   }
}
```

---

### **How Compiler Decides Which Method to Call?**

When you call the method:

* If you **pass no value** → calls method without parameter.
* If you **pass int** → calls int method.
* If you **pass string** → calls string method.
* Etc.

So **"input changes → output changes"**.

---

# **Relation with Polymorphism**

**Method Overloading comes under *Compile-Time Polymorphism*.**

### **Meaning of Polymorphism**

**Polymorphism = Behavior changes based on Input**

Just like:

* If we receive **good news**, we feel **happy**.
* If we receive **bad news**, we feel **sad**.

**Same person → different behaviors → based on input**
This is **polymorphism**.

In method overloading:

* Input means **parameters**.
* Output means **which method runs**.

---

### **Best Real Example – `IndexOf()` in String**

```csharp
string s = "Hello World";

s.IndexOf('o');        // Returns first occurrence → 4
s.IndexOf('o', 5);     // Start searching from index 5 → returns 7

s.IndexOf("ll");       // Search substring → returns 2
s.IndexOf("ll", 5);    // Search substring starting from index 5 → returns next occurrence
```

Same method name → **different behaviors** based on parameters.

---

# **Final Answer to Say in Interview**

> **Method Overloading is an approach of defining a method with multiple behaviors, where the behavior changes based on the parameters of the method.**
> The parameters can differ in:
>
> * number,
> * type,
> * or order.

That is why we use **method overloading**.

---

### **Example and Basic Idea**

* We already have a method in parent class.
* Child class wants **its own behavior** for that same method.
* So child class will **redefine** (override) the same method.

---

### **Syntax Concept**

```
class Parent
{
    public virtual void Test()  // parent method must be virtual
    {
        // Parent logic
    }
}

class Child : Parent
{
    public override void Test()  // child overrides it
    {
        // New logic (child logic)
    }
}
```

---

### **Why we need `virtual` and `override`?**

| Keyword    | Used In      | Meaning                                              |
| ---------- | ------------ | ---------------------------------------------------- |
| `virtual`  | Parent class | Parent is giving **permission** to child to override |
| `override` | Child class  | Child is **reimplementing** the parent method        |

**Without `virtual`, overriding is not possible.**

---

### **Simple Diagram**

```
       Parent Class
          |
   public virtual Test()
          |
        Inherited
          ↓
       Child Class
   public override Test()
```

Child **replaces** the behavior of parent’s method.

---

# **Difference Between Method Overloading & Method Overriding**

| Feature              | Overloading                                               | Overriding                                                 |
| -------------------- | --------------------------------------------------------- | ---------------------------------------------------------- |
| Meaning              | Same method name, **different parameters**                | Same method name, **same parameters**                      |
| Occurs In            | Can happen **within a class** or **between parent-child** | Can happen **only between parent-child**                   |
| Permission Needed?   | **No permission** needed                                  | **Child must take permission** from parent using `virtual` |
| Purpose              | **Multiple behaviors** for same method name               | **Change the behavior** of parent method                   |
| Runtime/Compile time | Compile-time polymorphism                                 | Runtime polymorphism                                       |

---

### **Example from script (Explained Cleanly)**

```csharp
class Parent
{
    public void Show()  // Normal non-virtual method
    {
        Console.WriteLine("Parent Show Method");
    }

    public virtual void Test()  // virtual → overridable
    {
        Console.WriteLine("Parent Test Method");
    }
}

class Child : Parent
{
    // Overloading Show() (changing parameters)
    public void Show(int x)
    {
        Console.WriteLine("Child Show Method");
    }

    // Overriding Test() (same parameters)
    public override void Test()
    {
        Console.WriteLine("Child Test Method");
    }
}
```

```csharp
static void Main()
{
    Child c = new Child();
    c.Show();      // Parent Show Method (inherited)
    c.Show(10);    // Child Show Method (overloaded)
    c.Test();      // Child Test Method (overridden)
}
```

---

# **Easy Understanding with Real-Life Example (from Script)**

Parent gives you a **mobile phone** as a gift.

Two choices:

1. **Use the phone as it is** → means use parent method directly.
2. **Exchange the phone** and take your liked model → means override parent method.

So:

* Parent method exists.
* Child **may** use it, **or may re-implement it**.

---

# **Key Line to Say in Interview**

> **Method Overriding is used to change the behavior of a parent class method in the child class.**
> For overriding, the method must be `virtual` in parent and `override` in child.

---


# **Method Hiding (Shadowing)**

**Method Hiding (Shadowing)** means:

> Re-implementing a **parent class method inside child class** exactly with the **same name & same signature**, **even when the parent method is not declared `virtual`**.

So overriding needs permission.
But **hiding does not need permission**.

---

### **Core Difference**

| Concept        | Keyword Used | Parent Method Must Be `virtual`? | What happens?                                         |
| -------------- | ------------ | -------------------------------- | ----------------------------------------------------- |
| **Overriding** | `override`   | **Yes**                          | Child replaces parent behavior (with permission)      |
| **Hiding**     | `new`        | **No**                           | Child replaces parent behavior **without permission** |

---

# **Example Code Used in Explanation**

```csharp
class ParentClass
{
    public virtual void Test1()     // Virtual method → can be overridden
    {
        Console.WriteLine("Test1 from Parent");
    }

    public void Test2()            // Non-virtual method → cannot be overridden
    {
        Console.WriteLine("Test2 from Parent");
    }
}

class ChildClass : ParentClass
{
    // Overriding Test1 (with permission)
    public override void Test1()
    {
        Console.WriteLine("Test1 from Child");
    }

    // Hiding Test2 (without permission)
    public new void Test2()
    {
        Console.WriteLine("Test2 from Child");
    }
}
```

```csharp
static void Main()
{
    ChildClass c = new ChildClass();
    c.Test1(); // Child
    c.Test2(); // Child
}
```

---

# **Why `new` keyword is used in hiding?**

* If we **don’t use `new`**, code still runs same.
* But **compiler gives a warning** saying:
  *“You are hiding a parent method. Use `new` if you intended to do so.”*

`new` is just **a confirmation** to compiler that:

> *Yes, I am intentionally replacing parent’s method.*

---

# **Important Behavior Difference (Very Important Interview Point)**

### **Case: Parent reference pointing to Child object**

```csharp
ParentClass p = new ChildClass();
p.Test1();   // Which one?
p.Test2();   // Which one?
```

| Method | Overriding / Hiding | Output                  |
| ------ | ------------------- | ----------------------- |
| Test1  | **Overridden**      | **Calls Child method**  |
| Test2  | **Hidden**          | **Calls Parent method** |

---

### **Why this happens?**

* **In Overriding:** Parent knows child is re-implementing (because of `virtual` & `override`). So parent reference can also call child method.
* **In Hiding:** Parent was **never informed** about child re-implementation. So parent reference will **not** call child method.

---

### **Diagram to Understand Clearly**

```
          METHOD OVERRIDING (With Permission)
          ----------------------------------
                ParentClass : Test1() virtual
                           ↓   allowed to override
                ChildClass : Test1() override

Parent Reference → Uses Child’s overridden method


          METHOD HIDING (Without Permission)
          ----------------------------------
                ParentClass : Test2() normal method
                           ↓   no override permission
                ChildClass : Test2() new

Parent Reference → Still uses Parent’s method
Child Reference → Uses Child’s method
```

---

# **Calling Parent Methods After Re-Implementation**

### **Two ways:**

#### **1) Create parent object in child**

```csharp
ParentClass p = new ParentClass();
p.Test1();   // Parent
p.Test2();   // Parent
```

#### **2) Use `base` keyword inside child**

```csharp
public void CallParentMethod()
{
    base.Test1();  // calls parent Test1
    base.Test2();  // calls parent Test2
}
```

*(Note: `base` cannot be used inside static blocks.)*

---

# **Very Important Line to Tell in Interview**

> **Method Overriding changes the behavior of parent method in child class with parent’s permission (`virtual` and `override`).
> Method Hiding changes the behavior without parent’s permission (`new` keyword).
> In overriding, parent reference calls child method.
> In hiding, parent reference calls parent method.**

---

# **Final Summary**

| Feature                   | Method Overriding       | Method Hiding (Shadowing)           |
| ------------------------- | ----------------------- | ----------------------------------- |
| Purpose                   | Change behavior         | Replace behavior without permission |
| Keywords                  | `virtual` + `override`  | `new`                               |
| Permission Needed         | **Yes**, from parent    | **No**                              |
| Parent Reference Behavior | Calls **Child Version** | Calls **Parent Version**            |
| Occurs Between            | Only Parent → Child     | Only Parent → Child                 |

---


# **Operator Overloading + Practical Use of Method Overriding**

---

## **First Recall – Method Overloading**

* **Method Overloading** = Same method name **but different parameters**.
* Used to give **multiple behaviors** to the **same method**.
* Behavior changes based on:

  * Number of parameters
  * Type of parameters
  * Order of parameters

### Example (Substring)

```csharp
s.Substring(14);         // from index to end
s.Substring(10, 3);      // from index, take certain characters
```

**Method name is same**, but **behavior differs** → This is method overloading.

---

# **Operator Overloading**

### **Definition**

Operator Overloading is:

> An approach of defining **multiple behaviors to an operator**, and the behavior changes based on **operand types**.

### Example (Already Happening in C#)

| Expression      | Operand Types   | Output Behavior          |
| --------------- | --------------- | ------------------------ |
| `10 + 20`       | int + int       | Addition (30)            |
| `"abc" + "xyz"` | string + string | Concatenation (`abcxyz`) |

So **operator is same**, but **behavior varies** depending on **operands**.
This itself is **operator overloading**.

---

## **How Computer Actually Performs + ?**

Computer **does not know** what `+` means.
Logic is written in **predefined operator methods** inside **.NET Libraries**.

### Example Internal Methods

```csharp
public static int operator +(int a, int b)
public static string operator +(string a, string b)
public static bool operator ==(string a, string b)
public static bool operator >(int a, int b)
```

So when we write:

```csharp
int z = x + y;
```

It **internally calls**:

```csharp
operator +(x, y)
```

---

# **Why We Need Operator Overloading in Our Own Classes?**

If we create our own class:

```csharp
Matrix m1, m2;
Matrix m3 = m1 + m2;   // ❌ ERROR
```

Compiler says:

```
operator + cannot be applied to operands of type Matrix and Matrix
```

Because **no operator method exists** for Matrix.

So we must **define it**.

---

# **Implementing Operator Overloading in Class**

### Matrix Class Structure

```csharp
class Matrix
{
   int a, b, c, d;

   public Matrix(int a, int b, int c, int d)
   {
      this.a = a; this.b = b;
      this.c = c; this.d = d;
   }
}
```

### Now Overload `+` Operator

```csharp
public static Matrix operator +(Matrix m1, Matrix m2)
{
   return new Matrix(
      m1.a + m2.a,
      m1.b + m2.b,
      m1.c + m2.c,
      m1.d + m2.d
   );
}
```

### Similarly Overload `-` Operator

```csharp
public static Matrix operator -(Matrix m1, Matrix m2)
{
   return new Matrix(
      m1.a - m2.a,
      m1.b - m2.b,
      m1.c - m2.c,
      m1.d - m2.d
   );
}
```

---

# **Output Problem – Why Matrix Was Printing Class Name?**

When we do:

```csharp
Console.WriteLine(m1);
```

It **calls**:

```csharp
ToString()
```

And default `ToString()` prints:

```
Name Of Class (Namespace.ClassName)
```

Because:

```
ToString() belongs to Object class
```

So behavior:

```
Console.WriteLine(m1);
    ↓
calls ToString()
    ↓
returns class name
```

---

# **Solution → Method Overriding (Practical Use Case)**

Since `ToString()` is **virtual** in Object class, we can **override** it.

### Override ToString() in Matrix Class

```csharp
public override string ToString()
{
   return a + " " + b + "\n" + c + " " + d + "\n";
}
```

Now `Console.WriteLine(m1);` prints Matrix values neatly.

---

## **Diagram (Very Important Point)**

```
                 Console.WriteLine(m1)
                           |
                           ↓
                Calls ToString() Method
                           |
           ---------------------------------
           |                               |
    If ToString() not overridden       If overridden in class
    → Print Class Name                 → Print Matrix Values
```

---

# **Final Understanding Summary**

| Concept              | Meaning                                               | When used                     |
| -------------------- | ----------------------------------------------------- | ----------------------------- |
| Method Overloading   | Same method name, different parameters                | Compile-Time Polymorphism     |
| Operator Overloading | Same operator, behavior changes based on operand type | Used in Custom Classes        |
| Method Overriding    | Child changes behavior of parent method               | Run-Time Polymorphism         |
| ToString() Override  | To display object data instead of class name          | Used for clean console output |

---

# **One-Line Interview Answer**

> **Operator Overloading allows us to define custom behavior for operators based on operand types.
> In our Matrix example, we overloaded `+` and `-` to add and subtract matrix values.
> To print Matrix values, we used Method Overriding on `ToString()`.**

---

