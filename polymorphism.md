
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

