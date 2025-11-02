### 1. **What is Visual Studio .NET**

* Visual Studio .NET is an **IDE (Integrated Development Environment)** provided by **Microsoft**.
* Used to **develop .NET applications** using multiple programming languages.
* It supports developing:

  * Console Applications
  * Windows Applications
  * Web Applications
  * Web Services
  * Windows Services
  * Mobile Applications

>  One IDE can be used to develop all types of applications — no need for multiple tools.

---

### 2. **.NET Framework**

* .NET is not a single language — it supports **multiple languages**:

  * C#
  * VB.NET
  * F#
  * J#
  * C++/CLI, etc.
* The same Visual Studio IDE can be used for all these languages.

---

### 3. **Starting Visual Studio**

* When you open Visual Studio, the **Start Page** appears first.
* The Start Page allows you to:

  * Create a **New Project**
  * **Open an Existing Project**
  * View **Recent Projects**

**Options on the Start Page:**

* **Keep page open after project loads**
* **Show page on startup**

---

### 4. **Creating a New Project**

Steps:

1. Click **File → New → Project**
2. In the **New Project Window**:

   * Select a language (e.g., Visual C#)
   * Choose a template (e.g., Console Application)
   * Give a **Project Name**
   * Specify **Location**
   * Optionally, give a **Solution Name**

> A *Solution* is a collection of one or more projects.
> A *Project* is a collection of items (classes, interfaces, forms, etc.).

---

### 5. **Understanding Solution Explorer**

* Found on the **right-hand side** of Visual Studio.
* Displays:

  * Solution (root)
  * Projects inside the solution
  * Files/classes inside each project
* If not visible → Go to **View → Solution Explorer**.

---

### 6. **Namespace and Class**

* Every project by default has:

  * A **namespace** (same as project name by default)
  * A **Program class** inside a file named `Program.cs`
* **Namespace:** A logical container to group related classes (not physical).

  * Similar to folders grouping files in OS.
* **Class:** Contains the actual code and logic.

---

### 7. **Using Statements**

* Example: `using System;`
* These are like **importing namespaces** — similar to `#include` in C/C++.
* Allow access to pre-defined classes from the .NET library.

---

### 8. **Writing and Running Code**

Example Program:

```csharp
using System;

namespace FirstProject
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World");
        }
    }
}
```

**Run Program:**

* Shortcut: `Ctrl + F5`
* Visual Studio compiles and executes the code.
* Output shown in a **console window** (`cmd.exe`).

If errors occur:

* Visual Studio shows **Error List** at the bottom.
* Always fix errors before re-running.

---

### 9. **Adding Another Class**

Steps:

1. Right-click on the Project → **Add → New Item**
2. Select **Class** template.
3. Give a class name (e.g., `Class1.cs`).
4. You can add as many classes as needed.

---

### 10. **Multiple Classes with Main Methods**

* If you have multiple classes with `Main()` methods:

  * Visual Studio shows **“Multiple entry points”** error.
* Fix:

  * Go to **Project Properties → Startup Object**
  * Choose which class’s `Main()` method should run.

---

### 11. **Common Issues**

* If your class does not appear in “Startup Object”:

  * The class does **not contain a Main method**, or
  * The **Main** method is written incorrectly.

**Correct Syntax:**

```csharp
static void Main(string[] args)
```

> “Main” must start with an uppercase ‘M’ because **C# is case-sensitive**.

---

### 12. **Windows and Panels in Visual Studio**

Common panels:

* **Solution Explorer**
* **Properties Window**
* **Toolbox**
* **Server Explorer**
* **Output Window**
* **Error List Window**

Each window can **auto-hide** to save space on the screen.

---
Here’s a clear and concise **note** based on your text:

---

## **Writing the First Program in C# using Notepad**

### **Step 1: Writing the Program**

Open **Notepad** and write the following code:

```csharp
class First
{
    static void Main()
    {
        System.Console.WriteLine("My first C# program.");
    }
}
```

---

### **Step 2: Saving the Program**

1. Create a folder named **“CSharp”** on any drive (e.g., D:\CSharp).
2. Save the file in this folder as **“First.cs”**

   * `.cs` is the extension for C# source files.

---

### **Step 3: Compilation of the Program**

To compile the program, use the **C# Compiler (`csc`)** from the **Developer Command Prompt for Visual Studio**.

#### **Procedure:**

1. Open **Developer Command Prompt for VS** from Windows Search.
2. Change directory to where your file is saved.
   Example:

   ```
   D:\> cd CSharp
   ```
3. Compile the program using:

   ```
   csc First.cs
   ```

   * If compilation is successful, an executable file **First.exe** is created in the same folder.
   * This file contains **CIL (Common Intermediate Language)** or **MSIL (Microsoft Intermediate Language)** code.

---

### **Step 4: Executing the Program**

To run the compiled program:

```
D:\CSharp> First
```

Output:

```
My first C# program.
```

---

## **Understanding the Program**

### **System.Console.WriteLine**

* **Console** is a **pre-defined class** in the **System namespace**.
* It provides **static methods** for input/output operations such as:

  * `WriteLine()` – Displays output on screen.
  * `Write()` – Prints output without a new line.
  * `Read()`, `ReadLine()`, `ReadKey()`, `Clear()` – For reading input or clearing the screen.
* Since these methods are **static**, they can be called directly using the class name:

  ```csharp
  System.Console.WriteLine("Hello");
  ```

---

### **System Namespace**

* A **namespace** is a **logical container** for related types such as:

  * Classes
  * Structures
  * Interfaces
  * Enums
  * Delegates

#### **Purposes of Namespaces:**

1. **Grouping Related Types**

   * Helps organize similar classes under one logical name.
2. **Avoiding Naming Conflicts**

   * Prevents errors when multiple classes have the same name.

**Example:**

```csharp
NSP1.First
NSP2.First
```

---

### **Importing Namespaces**

To avoid repeatedly writing the full namespace name, you can **import** a namespace using the **`using` directive**.

#### **Syntax:**

```csharp
using <namespace>;
```

#### **Examples:**

```csharp
using System;
using Microsoft.VisualBasic;
```

Each `using` statement should be written separately.

---

### **What is a Directive?**

* A **directive** is an **instruction to the compiler**.
* The `using` directive tells the compiler from which namespace to fetch the types used in the program.

---

### **Example: Importing a Namespace**

```csharp
using System;

class Second
{
    static void Main()
    {
        Console.Clear();
        Console.WriteLine("Importing a namespace.");
    }
}
```

Here, because `System` is imported, we can use `Console` directly without the `System.` prefix.

---

### **When Multiple Namespaces Have Same Type Name**

If two namespaces contain a type with the same name, you must use the **fully qualified name**:

```csharp
NSP1.First
NSP2.First
```

You cannot rely on `using` in this case.

---

## **Using the “using static” Directive**

### **Introduced in:** C# 6.0

This feature allows you to **import a specific type (class)** and access its **static members** directly **without prefixing the class name**.

#### **Syntax:**

```csharp
using static <namespace.type>;
```

#### **Example:**

```csharp
using static System.Console;

class Third
{
    static void Main()
    {
        Clear();
        WriteLine("Importing a type.");
    }
}
```

Here:

* We imported the **Console** class directly.
* We can use its static methods like `Clear()` and `WriteLine()` without writing `Console.` every time.

---


Here’s a **well-organized study note** based on your provided content about **Visual Studio and Project Creation in C#** 👇

---

# 💻 **Visual Studio – IDE for .NET Application Development**

## 🔹 **What is Visual Studio?**

Visual Studio (VS) is an **Integrated Development Environment (IDE)** used for developing **.NET applications** using languages such as **C#**, **VB.NET**, and others.
It supports creating various types of applications like:

* Console Applications
* Windows Applications
* Web Applications

> **Note:** The current version discussed here is **Visual Studio 2019 (version 16)**.

---

## 🧭 **Opening Visual Studio**

To open Visual Studio:

1. Go to **Windows Search**.
2. Type **Visual Studio 2019** and click to launch it.

---

## 🧱 **Creating a New Project**

Applications developed in Visual Studio are called **projects**.
Each project is a collection of files such as:

* Classes
* Interfaces
* Structures
* Enums
* Delegates
* HTML, XML, or text files

### Steps to Create a New Project:

1. Click **“Create a new project.”**
2. In the new window:

   * Under **All languages**, select **C#**.
   * Under **All platforms**, select **Windows**.
   * Under **All project types**, select **Console**.
3. Choose **“Console App (.NET Core)”** and click **Next**.
4. In the next window:

   * Enter **Project Name:** `FirstProject`
   * Set **Location:** `<drive>:\CSharp`
   * Click **Create**.

---

## 📄 **Default Code Generated**

A new file `Program.cs` is created by default with the following code:

```csharp
using System;

namespace FirstProject
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

### Explanation:

* When a project is created, all classes and types are placed inside a **namespace**.
* The namespace name is **same as the project name** (here, `FirstProject`).
* A **namespace** is a **logical container** for types like classes, structures, interfaces, enums, and delegates.

---

## ▶️ **Running the Program**

You can execute the program in two ways:

1. **Without Debugging:**

   * Press **Ctrl + F5**
   * Or go to **Debug → Start Without Debugging**
   * This will **save, compile, and run** the program and display output:

     ```
     Hello World!
     Press any key to continue . . .
     ```

2. **With Debugging:**

   * Press **F5**
   * Or go to **Debug → Start Debugging**
   * The program runs but the console window **closes immediately** after execution.
   * To keep it open, add:

     ```csharp
     Console.ReadLine();
     ```

---

## 🧩 **Adding New Items (Classes)**

To add a new class in the project:

1. Open **Solution Explorer** (right side panel).

   * If not visible → Go to **View → Solution Explorer**.
2. In Solution Explorer:

   * Right-click on the project name.
   * Select **Add → New Item → Class**.
   * Name it (e.g., `Class1.cs`) and click **Add**.

### Example Code in Class1:

```csharp
static void Main()
{
    Console.WriteLine("Second class under the project.");
    Console.ReadLine();
}
```

---

## ⚠️ **Handling Multiple Entry Points**

If your project has **more than one class** containing a `Main()` method, you’ll get an error:

> “Multiple entry points found.”

To fix this:

1. Open **Solution Explorer** → Right-click the project → Select **Properties**.
2. Under **Startup Object**, select the desired class (e.g., `FirstProject.Class1`).

If your class doesn’t appear:

* Open **Project File** (Right-click → Edit Project File).
* Locate the `<StartupObject>` tag and set it manually:

  ```xml
  <StartupObject>FirstProject.Class1</StartupObject>
  ```

---


