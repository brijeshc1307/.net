

##  Notes on Visual Studio .NET

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

> ✅ One IDE can be used to develop all types of applications — no need for multiple tools.

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

### ✅ **Summary**

* Visual Studio .NET = Microsoft IDE for .NET development.
* Supports multiple languages and project types.
* Organizes work in **Solutions** and **Projects**.
* **Namespace** groups classes logically.
* **Main()** is the program’s entry point.
* Use **Ctrl + F5** to build and run.
* Set **Startup Object** when multiple `Main()` methods exist.
* Fix errors using the **Error List** window.

---

Would you like me to format these notes into a **PDF or printable study sheet** (with headings and highlights)?
