Here’s a **well-organized and concise note** from your content — formatted for easy reading, revision, or class handouts.

---

#  **Data Types and Basic Concepts in C#**

---

## **1. Data Types in C#**

| **C# Type**                  | **IL Type**     | **Size/Capacity**       | **Default Value**                    |
| ---------------------------- | --------------- | ----------------------- | ------------------------------------ |
| **Integer Types**            |                 |                         |                                      |
| byte                         | System.Byte     | 1 byte (0–255)          | 0                                    |
| short                        | System.Int16    | 2 bytes (−2¹⁵ to 2¹⁵−1) | 0                                    |
| int                          | System.Int32    | 4 bytes (−2³¹ to 2³¹−1) | 0                                    |
| long                         | System.Int64    | 8 bytes (−2⁶³ to 2⁶³−1) | 0                                    |
| sbyte                        | System.SByte    | 1 byte (−128 to 127)    | 0                                    |
| ushort                       | System.UInt16   | 2 bytes (0–2¹⁶−1)       | 0                                    |
| uint                         | System.UInt32   | 4 bytes (0–2³²−1)       | 0                                    |
| ulong                        | System.UInt64   | 8 bytes (0–2⁶⁴−1)       | 0                                    |
| **Decimal Types**            |                 |                         |                                      |
| float                        | System.Single   | 4 bytes                 | 0                                    |
| double                       | System.Double   | 8 bytes                 | 0                                    |
| decimal                      | System.Decimal  | 16 bytes                | 0                                    |
| **Boolean Type**             |                 |                         |                                      |
| bool                         | System.Boolean  | 1 byte                  | false                                |
| **Date & Unique Types**      |                 |                         |                                      |
| DateTime                     | System.DateTime | 8 bytes                 | 01/01/0001 00:00:00                  |
| Guid                         | System.Guid     | 32 bytes                | 00000000-0000-0000-0000-000000000000 |
| **Character & String Types** |                 |                         |                                      |
| char                         | System.Char     | 2 bytes                 | '\0'                                 |
| string                       | System.String   | Variable                | null                                 |
| **Base Type**                |                 |                         |                                      |
| object                       | System.Object   | Variable                | null                                 |

---

### **Key Points**

* All above are **primitive or predefined types** defined under **System namespace**.
* After compilation, all C# types convert to **IL (Intermediate Language)** types.

  * **String & Object** → classes
  * Other 15 → structures
* Signed types: `short, int, long, sbyte`
* Unsigned types: `ushort, uint, ulong, byte`
* `Guid` is used to store **unique identifiers** (32-byte alphanumeric).
* `char` supports **Unicode**, hence 2 bytes.
* `string` and `object` are **variable-length** types.
* `object` is the **parent of all types** and can store any value.

---

## **2. Declaring Fields & Variables**

**Syntax:**

```csharp
[<modifiers>] [const] [readonly] <type> <name> [= default value] [, ...];
```

**Example:**

```csharp
class Test {
    int x; // Field (Global scope)
    static void Main() {
        int x = 100; // Variable (Local scope)
    }
}
```

**Default Values:**

| Type           | Default                              |
| -------------- | ------------------------------------ |
| Numeric        | 0                                    |
| bool           | false                                |
| char           | '\0'                                 |
| Guid           | 00000000-0000-0000-0000-000000000000 |
| DateTime       | 01/01/0001 00:00:00                  |
| string, object | null                                 |

> ⚠️ Variables **must** be initialized before use (no default value).

---

### **Modifiers**

Define scope/access:

* `private` (default)
* `public`
* `internal`
* `protected`

---

### **Constants and Readonly**

```csharp
const float pi = 3.14f;    // Constant - must be initialized
readonly float pi;         // Readonly - can be assigned later
pi = 3.14f;
```

> Decimal literals must be suffixed:
> `f` → float, `m` → decimal
> Example: `float pi = 3.14f; decimal d = 3.14m;`

---

## **3. Categories of Data Types**

### **(1) Value Types**

* **Stored on:** Stack
* **Examples:** int, float, bool, char, DateTime, Guid
* **Fixed size** memory
* Each program gets its **own stack** (FILO/LIFO).

### **(2) Reference Types**

* **Stored on:** Heap
* **Examples:** string, object
* Heap supports **dynamic memory management**.
* Managed by **Garbage Collector (GC)**.

---

## **4. Nullable Value Types**

Normally, value types cannot store `null`.
To make them nullable, use `?` after type.

```csharp
int? i = null;
decimal? d = null;
```

---

## **5. Implicitly Typed Variables (`var`)**

Introduced in **C# 3.0**
Type is inferred from the assigned value.

```csharp
var i = 100;     // int
var f = 3.14f;   // float
var b = true;    // bool
var s = "Hello"; // string
```

**Restrictions:**

1. Must be initialized at declaration.
2. Can be used only for **local variables**, not fields.

---

## **6. Dynamic Type (`dynamic`)**

Introduced in **C# 4.0**

| **Feature**             | **var**      | **dynamic** |
| ----------------------- | ------------ | ----------- |
| Type checking           | Compile-time | Run-time    |
| Can change type later   | ❌            | ✅           |
| Initialization required | ✅            | ❌           |
| Can be used for fields  | ❌            | ✅           |

**Example:**

```csharp
dynamic d;
d = 100;    // int
d = "Hi";   // string
d = false;  // bool
```

---

## **7. Boxing & Unboxing**

**Boxing:** Converting value type → reference type

```csharp
int i = 100;
object obj = i; // Boxing
```

**Unboxing:** Reference type → value type

```csharp
int j = Convert.ToInt32(obj); // Unboxing
```

> ✅ Use `Convert.To<Type>()` methods like `ToDouble`, `ToBoolean`, etc.

---

## **8. Taking Input from User**

```csharp
Console.Write("Enter 1st number: ");
double d1 = Convert.ToDouble(Console.ReadLine());
Console.Write("Enter 2nd number: ");
double d2 = double.Parse(Console.ReadLine());
Console.WriteLine($"Sum of {d1} & {d2} is: {d1 + d2}");
```

### **Console.ReadLine()**

* Waits for user input
* Reads input
* Returns it as **string**

**Conversion Methods:**

* `Convert.ToDouble(string)`
* `double.Parse(string)`

---

## **9. String Interpolation (C# 6.0+)**

```csharp
Console.WriteLine($"Sum of {d1} and {d2} is {d3}");
```

> Easier and cleaner than composite formatting (`{0}`, `{1}`).

---

## **10. Operators in C#**

| **Category**  | **Operators**                                  |   |        |
| ------------- | ---------------------------------------------- | - | ------ |
| Arithmetic    | `+`, `-`, `*`, `/`, `%`                        |   |        |
| Assignment    | `=`, `+=`, `-=`, `*=`, `/=`, `%=`              |   |        |
| Relational    | `==`, `!=`, `<`, `<=`, `>`, `>=`               |   |        |
| Logical       | `&&`, `                                        |   | `, `!` |
| Unary         | `++`, `--`                                     |   |        |
| Miscellaneous | `sizeof()`, `typeof()`, `is`, `as`, `?:`, `??` |   |        |

---

## **11. Conditional Statements**

### **(a) if–else Statement**

```csharp
if (condition)
    statement;
else if (condition)
    statement;
else
    statement;
```

**Example:**

```csharp
if (d1 > d2)
    Console.WriteLine("1st number is greater.");
else if (d1 < d2)
    Console.WriteLine("2nd number is greater.");
else
    Console.WriteLine("Both numbers are equal.");
```

---

### **(b) switch–case Statement**

```csharp
switch (expression) {
    case value1:
        statement;
        break;
    case value2:
        statement;
        break;
    default:
        statement;
        break;
}
```

**Example:**

```csharp
switch(Sno) {
    case 1: Console.WriteLine("Student 1"); break;
    case 2: Console.WriteLine("Student 2"); break;
    case 3: Console.WriteLine("Student 3"); break;
    default: Console.WriteLine("No student exists."); break;
}
```

> 🔹 `break` is **mandatory** in C# after every case (including `default`).

---

### ✅ **Summary**

| **Concept**          | **Key Point**                      |
| -------------------- | ---------------------------------- |
| Primitive Types      | Defined under `System` namespace   |
| Value vs Reference   | Stack vs Heap                      |
| Nullable Types       | Allow null for value types         |
| var                  | Compile-time type inference        |
| dynamic              | Run-time type inference            |
| Boxing/Unboxing      | Value ↔ Reference conversion       |
| ReadLine             | Reads user input as string         |
| String Interpolation | Easier string formatting           |
| Operators            | Perform mathematical/logical tasks |
| Conditionals         | Control flow of program            |

---

Would you like me to convert this into a **printable formatted PDF handout** (with table borders, syntax boxes, and highlighted examples)?
