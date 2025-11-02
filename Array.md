Here’s a **well-organized and easy-to-study note** based on your provided material 👇

---

# 📘 **Arrays in C#**

---

## 🔹 **Definition**

An **Array** is a collection of *similar type elements* stored in **sequential order** — either in a single row or in rows and columns.

* In C#, array elements are accessed using an **index** starting from **0** up to **(n - 1)**.
* Arrays can be of **fixed length** or **dynamic**:

  * **Fixed-length array** → size is defined at creation.
  * **Dynamic array** → size can increase when new items are added.

---

## 🔸 **1-Dimensional Arrays**

Used to store data in a single row.

**Syntax:**

```csharp
<type>[] <array_name> = new <type>[size];
```

**Examples:**

```csharp
int[] arr = new int[5];              // Declaration + Initialization
int[] arr;                           // Declaration only
arr = new int[5];                    // Initialization later
int[] arr = { 10, 20, 30, 40, 50 };  // With predefined values
```

---

### ✅ **Example Program:**

```csharp
using System;
class SDArray1 {
    static void Main() {
        Console.Clear();
        int x = 0;
        int[] arr = new int[6];

        // Accessing default values using for loop
        for(int i = 0; i < 6; i++)
            Console.Write(arr[i] + " ");
        Console.WriteLine();

        // Assigning values using for loop
        for(int i = 0; i < 6; i++) {
            x += 10;
            arr[i] = x;
        }

        // Accessing values using foreach loop
        foreach(int i in arr)
            Console.Write(i + " ");
        Console.WriteLine();
    }
}
```

---

## 🔹 **for Loop vs foreach Loop (Array Access)**

| **Feature**                 | **for loop**        | **foreach loop**             |
| --------------------------- | ------------------- | ---------------------------- |
| **Loop variable refers to** | Index of the array  | Value of the array           |
| **Can assign values?**      | ✅ Yes               | ❌ No (Read-only)             |
| **Loop variable type**      | Always `int`        | Same as array’s element type |
| **Use case**                | Reading and writing | Reading only                 |

---

**Example:**

```csharp
int[] iarr = { 10, 20, 30, 40, 50 };
double[] darr = { 12.34, 34.56, 56.78, 78.90, 90.12 };
string[] sarr = { "Red", "Blue", "Green", "Yellow", "Magenta" };
```

Using `for` and `foreach`:

```csharp
for (int i = 0; i < iarr.Length; i++)
    Console.WriteLine(iarr[i]);

foreach (int i in iarr)
    Console.WriteLine(i);
```

---

## 🔹 **Array Class (System.Array)**

`Array` is a predefined class under the **System** namespace that provides methods and properties to manipulate arrays.

| **Member**                           | **Type** | **Description**                     |
| ------------------------------------ | -------- | ----------------------------------- |
| `Sort(Array arr)`                    | Method   | Sorts the array in ascending order  |
| `Reverse(Array arr)`                 | Method   | Reverses the order of elements      |
| `Copy(Array src, Array dest, int n)` | Method   | Copies first `n` elements           |
| `GetLength(int dimension)`           | Method   | Returns size of the given dimension |
| `Length`                             | Property | Returns total number of elements    |

---

**Example:**

```csharp
using System;
class SDArray2 {
    static void Main() {
        Console.Clear();
        int[] arr = { 54, 79, 59, 8, 42, 22, 93, 3, 73, 38, 67, 48, 18, 61, 32, 86, 15, 27, 81, 96 };

        Array.Sort(arr);
        foreach (int i in arr)
            Console.Write(i + " ");
        Console.WriteLine();

        Array.Reverse(arr);
        foreach (int i in arr)
            Console.Write(i + " ");
        Console.WriteLine();

        int[] brr = new int[10];
        Array.Copy(arr, brr, 7);
        foreach (int i in brr)
            Console.Write(i + " ");
        Console.WriteLine();
    }
}
```

---

## 🔸 **2-Dimensional Arrays**

Used to store data in **rows and columns**.

**Syntax:**

```csharp
<type>[,] <array_name> = new <type>[rows, columns];
```

**Example:**

```csharp
int[,] arr = new int[4, 5];
```

### ✅ Accessing and Assigning Values

```csharp
for (int i = 0; i < arr.GetLength(0); i++) {
    for (int j = 0; j < arr.GetLength(1); j++)
        Console.Write(arr[i, j] + " ");
    Console.WriteLine();
}
```

**Initialization at declaration:**

```csharp
int[,] arr = {
    { 11, 12, 13, 14, 15 },
    { 21, 22, 23, 24, 25 },
    { 31, 32, 33, 34, 35 },
    { 41, 42, 43, 44, 45 }
};
```

---

## 🔸 **Jagged Arrays (Array of Arrays)**

Jagged arrays are **arrays of arrays** where each row can have a different number of columns.

**Syntax:**

```csharp
<type>[][] <array_name> = new <type>[rows][];
```

**Example:**

```csharp
int[][] arr = new int[4][];
arr[0] = new int[5];
arr[1] = new int[6];
arr[2] = new int[8];
arr[3] = new int[4];
```

### ✅ Accessing and Assigning Values

```csharp
for (int i = 0; i < arr.GetLength(0); i++) {
    for (int j = 0; j < arr[i].Length; j++)
        arr[i][j] = i + 1;
}
```

### Access using `foreach`:

```csharp
foreach (int[] row in arr) {
    foreach (int val in row)
        Console.Write(val + " ");
    Console.WriteLine();
}
```

**Initialization at declaration:**

```csharp
int[][] arr = {
    new int[5] { 11, 12, 13, 14, 15 },
    new int[6] { 21, 22, 23, 24, 25, 26 },
    new int[8] { 31, 32, 33, 34, 35, 36, 37, 38 },
    new int[4] { 41, 42, 43, 44 }
};
```

---

## 🔸 **Implicitly Typed Arrays**

We can use the `var` keyword to declare arrays whose type is inferred from the assigned values.

**Examples:**

```csharp
var iarr = new[] { 10, 20, 30, 40, 50 };        // int array
var sarr = new[] { "Red", "Blue", "Green" };    // string array
var darr = new[] { 12.34, 34.56, 56.78, 78.90 }; // double array
```

**Implicitly typed jagged array:**

```csharp
var jarr = new[] {
    new[] { 11, 12, 13, 14, 15 },
    new[] { 21, 22, 23, 24, 25, 26 },
    new[] { 31, 32, 33, 34, 35, 36 },
    new[] { 41, 42, 43, 44 }
};
```

---

## 🧩 **Command-Line Arguments**

* Values passed to the program through the **Main() method’s parameters**.
* The `Main()` method can accept an **array of strings** (`string[] args`).

**Example:**

```csharp
using System;
class Params {
    static void Main(string[] args) {
        foreach (string str in args)
            Console.WriteLine(str);
    }
}
```

**Execution:**

```bash
C:\CSharp> Params 100 Hello 34.56 A true
```

Output:

```
100
Hello
34.56
A
true
```

---

### ✅ **Example: Adding Command-Line Numbers**

```csharp
using System;
class AddParams {
    static void Main(string[] args) {
        double Sum = 0;
        foreach (string str in args)
            Sum += double.Parse(str);
        Console.WriteLine("Sum of given {0} numbers is: {1}", args.Length, Sum);
    }
}
```

---
Perfect 👍 Here’s how to **write a clean and structured note** explaining the *execution of a C# program using Command-Line Arguments*, including your given examples:

---

# 💻 **Executing C# Programs with Command-Line Arguments**

After compiling a C# program, you can execute it through the **Command Prompt (CMD)** by passing **arguments** (inputs) directly after the program name.

These arguments are captured in the `string[] args` parameter of the `Main()` method.

---

## 🔹 **Example Program**

```csharp
using System;
class AddParams {
    static void Main(string[] args) {
        double Sum = 0;
        foreach (string str in args)
            Sum = Sum + double.Parse(str);
        Console.WriteLine("Sum of given {0} numbers is: {1}", args.Length, Sum);
    }
}
```

### 🔸 **Explanation**

* `args` → Stores all values passed from the command line as strings.
* `double.Parse(str)` → Converts each string argument into a double value.
* The loop adds all values and displays the result.

---

## ⚙️ **How to Execute from Command Prompt**

Once your program is compiled (for example, `AddParams.cs` → `AddParams.exe`), open the **Command Prompt** and navigate to the directory where the `.exe` file is located.

Then, run the program as shown below 👇

---

###  **Execution Examples**

```
<drive>:\CSharp> AddParams 10 20 30 ⏎
```

**Output:**

```
Sum of given 3 numbers is: 60
```

---

```
<drive>:\CSharp> AddParams 34.56 28.93 98.45 63.28 ⏎
```

**Output:**

```
Sum of given 4 numbers is: 225.22
```

---

```
<drive>:\CSharp> AddParams 938.387 534 348.378 836 174.392 ⏎
```

**Output:**

```
Sum of given 5 numbers is: 2830.157
```

---

```
<drive>:\CSharp> AddParams 18 48.37 75 56.43 97 85.19 ⏎
```

**Output:**

```
Sum of given 6 numbers is: 379.99
```

---


