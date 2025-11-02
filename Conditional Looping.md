Here’s a clear, well-structured **note on Conditional Looping and Jump Statements in C#**, summarizing all the important concepts and examples from your content 👇

---

# 🔁 **Conditional Looping and Jump Statements in C#**

---

## **1. Conditional Looping**

C# provides **4 types of loops** that execute a block of code repeatedly until a given condition is met:

1. `for` loop
2. `while` loop
3. `do..while` loop
4. `foreach` loop

---

### **Common Parts of a Loop**

Every loop requires 3 key components:

1. **Initialization** → sets the starting point
2. **Condition** → determines when to stop
3. **Iteration** → updates the loop variable (move forward or backward)

---

## **2. for Loop**

**Syntax:**

```csharp
for (initializer; condition; iteration)
{
    // Statements
}
```

**Example:**

```csharp
for (int i = 1; i <= 100; i++)
{
    Console.WriteLine(i);
}
```

👉 **Notes:**

* Initialization happens only once at the beginning.
* The loop runs as long as the **condition** is true.
* After each iteration, the **iteration expression** (like `i++`) executes.
* Minimum executions = **0**, if condition is false initially.

---

## **3. while Loop**

**Syntax:**

```csharp
while (condition)
{
    // Statements
}
```

**Example:**

```csharp
int i = 1;
while (i <= 100)
{
    Console.WriteLine(i);
    i++;
}
```

👉 **Notes:**

* Condition is tested **before** entering the loop.
* If condition is false initially, loop body **won’t execute** at all.

---

## **4. do..while Loop**

**Syntax:**

```csharp
do
{
    // Statements
}
while (condition);
```

**Example:**

```csharp
int i = 1;
do
{
    Console.WriteLine(i);
    i++;
}
while (i <= 100);
```

👉 **Notes:**

* Loop executes **at least once**, even if condition is false initially.
* Condition is checked **after** executing the body.
* Minimum executions = **1**.

---

## **5. foreach Loop**

Used for iterating over **arrays or collections**.

**Syntax:**

```csharp
foreach (type variable in array_or_collection)
{
    // Statements
}
```

**Example:**

```csharp
string[] names = { "A", "B", "C" };
foreach (string n in names)
{
    Console.WriteLine(n);
}
```

👉 **Note:**

* `foreach` automatically iterates through all elements without needing explicit indexing.
* Cannot modify the collection while iterating.

---

# 🧭 **Jump Statements in C#**

Jump statements are used to **transfer program control** from one point to another.

C# provides 4 types:

1. `goto`
2. `break`
3. `continue`
4. `return`

---

## **1. goto Statement**

Transfers control to a **labelled statement** within the same method.

**Syntax & Example:**

```csharp
goto label;
Console.WriteLine("Hello World");

label:
Console.WriteLine("Goto Called.");
```

👉 **Note:**
Use sparingly—can make code hard to read.

---

## **2. break Statement**

* Used to **exit immediately** from:

  * Loops (`for`, `while`, `do..while`, `foreach`)
  * `switch` statements

**Example:**

```csharp
for (int i = 1; i <= 100; i++)
{
    Console.WriteLine(i);
    if (i == 50)
        break;
}
Console.WriteLine("End of the loop.");
```

👉 After `break`, control moves to the first statement **after** the loop.

---

## **3. continue Statement**

* Skips the remaining statements in the current iteration
* Moves directly to the **next iteration**

**Example:**

```csharp
for (int i = 1; i <= 100; i++)
{
    if (i == 7 || i == 77)
        continue;
    Console.WriteLine(i);
}
```

👉 **Note:**
Unlike `break`, it **doesn’t exit** the loop — just skips the current pass.

---

## **4. return Statement**

* Terminates the execution of the **current method**
* Optionally returns a value to the caller

**Example Program:**

```csharp
using System;
class Table
{
    static void Main()
    {
        Console.Write("Enter a number: ");
        bool status = uint.TryParse(Console.ReadLine(), out uint x);

        if (status == true)
        {
            if (x == 0)
                return; // Terminates the method immediately

            Console.Clear();
            for (uint i = 1; i <= 10; i++)
            {
                Console.WriteLine("{0} * {1} = {2}", x, i, x * i);
            }
        }
        else
            Console.WriteLine("Please enter an unsigned integer value as input.");
    }
}
```

👉 **Explanation:**

* `uint.TryParse()` safely converts input to an unsigned integer.
* If input is invalid or zero, `return` exits the `Main()` method immediately.

---

# ✅ **Summary Table**

| **Concept**      | **Purpose**                      | **Key Point**                        |
| ---------------- | -------------------------------- | ------------------------------------ |
| `for` loop       | Repeats a block with known range | Initialization, condition, iteration |
| `while` loop     | Checks condition before loop     | May execute 0 times                  |
| `do..while` loop | Executes at least once           | Condition checked after body         |
| `foreach` loop   | Iterates collections             | Read-only iteration                  |
| `goto`           | Jumps to labeled line            | Avoid overuse                        |
| `break`          | Exits loop or switch             | Ends current loop immediately        |
| `continue`       | Skips current iteration          | Jumps to next loop cycle             |
| `return`         | Ends method execution            | Can return value                     |

---

Would you like me to include **flow diagrams** (for vs while vs do-while) in the next version of this note? They can help visualize how the loops operate step-by-step.
