

### **1) What is Garbage Collection (GC)**

Garbage Collection is a **memory management process** in .NET that automatically frees memory occupied by objects that are no longer in use, helping prevent memory leaks.

* **How it works:**

  1. The .NET runtime keeps track of object references.
  2. If an object is no longer referenced, it's considered *garbage*.
  3. GC cleans these objects and frees memory.

* **Generations:**

  * **Gen 0:** Short-lived objects.
  * **Gen 1:** Objects surviving Gen 0.
  * **Gen 2:** Long-lived objects like static objects.

* **Manual triggering:** `GC.Collect()`, but generally not recommended.

**Example:**

```csharp
class Program {
    static void Main() {
        MyClass obj = new MyClass();
        obj = null; // eligible for GC
        GC.Collect(); // force collection
    }
}
class MyClass {
    ~MyClass() { Console.WriteLine("Finalizer called"); }
}
```

---

### **2) Difference between Managed & Unmanaged Code**

| Feature           | Managed Code                  | Unmanaged Code      |
| ----------------- | ----------------------------- | ------------------- |
| Execution         | Runs under CLR                | Runs directly on OS |
| Memory Management | Automatic via GC              | Manual              |
| Safety            | Type-safe, secure             | Less secure         |
| Language          | C#, VB.NET                    | C, C++              |
| Example           | `Console.WriteLine("Hello");` | `printf("Hello");`  |

* **Managed Code:** Handled by **.NET CLR**, type-safe, automatic memory management.
* **Unmanaged Code:** Traditional programming, needs manual memory management.

---

### **3) What is Dependency Injection (DI) & its Types**

**DI** is a **design pattern** where dependencies (services, objects) are **injected** rather than created inside a class. This promotes **loose coupling** and **testability**.

* **Types:**

  1. **Constructor Injection:** Injected through constructor.
  2. **Property Injection:** Injected via property.
  3. **Method Injection:** Injected as method parameters.

**Example:**

```csharp
public interface IMessageService { void Send(string msg); }
public class EmailService : IMessageService {
    public void Send(string msg) => Console.WriteLine("Email: " + msg);
}
public class Notification {
    private IMessageService _service;
    public Notification(IMessageService service) { _service = service; }
    public void Notify(string msg) => _service.Send(msg);
}
```

* Here `EmailService` is injected into `Notification`.

---

### **4) Difference between `Finalize` & `Dispose`**

| Feature       | Finalize                     | Dispose                               |
| ------------- | ---------------------------- | ------------------------------------- |
| Purpose       | Cleanup unmanaged resources  | Cleanup managed & unmanaged resources |
| Call          | Called by GC automatically   | Called manually by developer          |
| Syntax        | `~ClassName()`               | Implements `IDisposable.Dispose()`    |
| Deterministic | No (depends on GC)           | Yes                                   |
| Example       | File handles, DB connections | Preferred for deterministic cleanup   |

**Usage:**

```csharp
class Resource : IDisposable {
    public void Dispose() { Console.WriteLine("Dispose called"); }
    ~Resource() { Console.WriteLine("Finalize called"); }
}
```

* `Dispose()` is preferred over finalizers for **manual and timely cleanup**.

---

### **5) Explain MVC Model**

**MVC (Model-View-Controller)** is a **design pattern** used in ASP.NET for **separation of concerns**:

1. **Model:** Represents data & business logic.
2. **View:** UI or presentation layer.
3. **Controller:** Handles user input, interacts with model, returns view.

**Flow:**

* User → Controller → Model → Controller → View → User

**Example:**

```csharp
public class ProductController : Controller {
    public IActionResult Index() {
        var products = ProductRepository.GetAll();
        return View(products);
    }
}
```

---

### **6) Explain MVVM Model**

**MVVM (Model-View-ViewModel)** is used in **WPF/Xamarin**:

1. **Model:** Data & business logic.
2. **View:** UI elements.
3. **ViewModel:** Acts as a bridge between Model & View, supports **data binding**.

* **Key:** Two-way data binding (`INotifyPropertyChanged`).

**Example:**

```csharp
public class PersonViewModel : INotifyPropertyChanged {
    public string Name { get; set; }
    public event PropertyChangedEventHandler PropertyChanged;
}
```

---

### **7) What are Filters in ASP.NET MVC & Order of Execution**

**Filters** allow code to run **before/after action methods**.

* Types:

  1. **Authorization filters** → `OnAuthorization`
  2. **Action filters** → `OnActionExecuting`, `OnActionExecuted`
  3. **Result filters** → `OnResultExecuting`, `OnResultExecuted`
  4. **Exception filters** → `OnException`

**Order of Execution:**

1. Authorization
2. Action
3. Result
4. Exception (if any)

---

### **8) What is Web API**

* Web API is a framework for building **HTTP services** in .NET.
* Allows RESTful APIs using `Controller` classes.
* Returns **JSON/XML**, not necessarily Views.

**Example:**

```csharp
[ApiController]
[Route("api/[controller]")]
public class ProductsController : ControllerBase {
    [HttpGet]
    public IEnumerable<string> Get() => new string[] { "Product1", "Product2" };
}
```

---

### **9) HTTP Verbs in Web API**

* **GET:** Fetch data
* **POST:** Create new resource
* **PUT:** Update existing resource
* **DELETE:** Delete resource
* **PATCH:** Partial update

---

### **10) What is CLR, CTS, JIT**

1. **CLR (Common Language Runtime):** Executes .NET code, provides memory management, security, exception handling.
2. **CTS (Common Type System):** Standardizes data types across .NET languages.
3. **JIT (Just-In-Time compiler):** Converts MSIL to native code at runtime.

---

### **11) Difference between Interface & Abstraction**

| Feature          | Interface                            | Abstract Class                |
| ---------------- | ------------------------------------ | ----------------------------- |
| Inheritance      | Multiple                             | Single                        |
| Methods          | Only declarations (C# 7 and earlier) | Can have concrete & abstract  |
| Fields           | Cannot have fields                   | Can have fields               |
| Access Modifiers | Public only                          | Can have protected/private    |
| Use              | Contract for classes                 | Base for shared functionality |

---

### **12) Explain Pillars of OOP (C#)**

1. **Encapsulation:** Hiding internal state, exposing behavior via methods.
2. **Abstraction:** Exposing essential features only.
3. **Inheritance:** Reusing base class properties/methods.
4. **Polymorphism:** Ability to take many forms (`virtual`, `override`, `interface`).

---

### **13) Delegates & Types**

* **Delegate:** Type-safe pointer to methods.
* **Types:**

  1. **Single-cast:** Points to single method
  2. **Multicast:** Points to multiple methods
  3. **Func/Action/Predicate:** Built-in generic delegates

**Example:**

```csharp
public delegate void Notify(string message);
Notify n = msg => Console.WriteLine(msg);
n("Hello Delegate!");
```

---

### **14) Difference between Array & ArrayList**

| Feature              | Array          | ArrayList                    |
| -------------------- | -------------- | ---------------------------- |
| Type                 | Strongly typed | Stores objects (non-generic) |
| Size                 | Fixed          | Dynamic                      |
| Performance          | Faster         | Slower (boxing/unboxing)     |
| Namespace            | System         | System.Collections           |
| Generics Alternative | List<T>        | -                            |

---

### **15) Difference between `var` & `dynamic`**

| Feature | var                        | dynamic                         |
| ------- | -------------------------- | ------------------------------- |
| Type    | Determined at compile-time | Determined at runtime           |
| Safety  | Type-safe                  | Not type-safe                   |
| Example | `var x = 10;`              | `dynamic y = 10; y = "string";` |

---

### **16) Difference between .NET Framework & .NET Core**

| Feature     | .NET Framework  | .NET Core                     |
| ----------- | --------------- | ----------------------------- |
| Platform    | Windows only    | Cross-platform                |
| Deployment  | Installed on OS | Self-contained deployment     |
| Performance | Slower          | Faster                        |
| Open-source | Partial         | Fully open-source             |
| Versions    | Legacy          | Active development (.NET 7/8) |

---

Absolutely, Brijesh! Let’s go **deep dive** into each of your new .NET/C# topics with clear explanations, examples, and usage scenarios.

---

### **18) What is `async` & `await` keywords**

* **Purpose:** Simplify **asynchronous programming** in C# to avoid blocking the main thread.
* **`async`:** Marks a method as asynchronous, allowing `await` inside it.
* **`await`:** Pauses the method execution until the awaited task completes, **without blocking the thread**.

**Example:**

```csharp
public async Task<string> GetDataAsync() {
    await Task.Delay(2000); // simulate delay
    return "Data loaded";
}

static async Task Main() {
    string result = await GetDataAsync();
    Console.WriteLine(result);
}
```

* Used in **Web API**, **WPF**, and any **I/O-bound operations**.

---

### **15) Explain Multithreading**

* **Multithreading:** Running multiple threads concurrently in a program.
* **Purpose:** Improves performance by using CPU cores efficiently.
* **Thread Management in C#:**

  * `Thread` class
  * `Task` Parallel Library (TPL)
  * Async/await (higher-level abstraction)

**Example:**

```csharp
Thread t = new Thread(() => {
    for(int i=0; i<5; i++)
        Console.WriteLine("Thread running");
});
t.Start();
```

* **Thread synchronization:** `lock`, `Mutex`, `Semaphore` to avoid **race conditions**.

---

### **20) What are Design Patterns**

* **Design Patterns:** Reusable solutions to common software design problems.
* **Types:**

  1. **Creational:** Object creation (`Singleton`, `Factory`, `Builder`)
  2. **Structural:** Object composition (`Adapter`, `Decorator`, `Facade`)
  3. **Behavioral:** Object interaction (`Observer`, `Strategy`, `Command`)

**Example (Singleton):**

```csharp
public class Singleton {
    private static Singleton _instance;
    private Singleton() {}
    public static Singleton Instance => _instance ??= new Singleton();
}
```

---

### **21) Caching, Session, View, State Management in ASP.NET**

| Feature               | Description                                                                        |
| --------------------- | ---------------------------------------------------------------------------------- |
| **Caching**           | Store frequently used data to reduce DB calls (`MemoryCache`, `OutputCache`)       |
| **Session**           | Stores per-user data on server, lives till session expires (`HttpContext.Session`) |
| **ViewState**         | Stores data in a hidden field on page, specific to page lifecycle                  |
| **Application State** | Shared across all users, server-wide storage (`HttpContext.Application`)           |

**Example (Session):**

```csharp
HttpContext.Session.SetString("Username", "Brijesh");
string user = HttpContext.Session.GetString("Username");
```

---

### **22) Explain ViewBag, ViewData, TempData**

| Feature  | ViewBag                    | ViewData                       | TempData                      |
| -------- | -------------------------- | ------------------------------ | ----------------------------- |
| Type     | Dynamic                    | Dictionary                     | Dictionary                    |
| Lifetime | Current request            | Current request                | Persist across 1 redirect     |
| Syntax   | `ViewBag.Name = "Brijesh"` | `ViewData["Name"] = "Brijesh"` | `TempData["Msg"] = "Hello"`   |
| Use      | Passing data to View       | Passing data to View           | Passing data between requests |

---

### **23) Authentication & Authorization**

* **Authentication:** Verify **who the user is**.

  * Techniques: Forms, JWT, OAuth, IdentityServer
* **Authorization:** Verify **what user can access**.

  * Techniques: Role-based, Policy-based, Claims-based

**Example:**

```csharp
[Authorize(Roles="Admin")]
public IActionResult AdminPage() { return View(); }
```

---

### **24) What is Middleware**

* **Middleware:** Software components in ASP.NET Core pipeline that handle **HTTP requests/responses**.
* Executes in **order** during request and response.
* Examples: `Authentication`, `Routing`, `Exception Handling`

**Example:**

```csharp
app.Use(async (context, next) => {
    Console.WriteLine("Request Incoming");
    await next.Invoke();
    Console.WriteLine("Response Outgoing");
});
```

---

### **25) What is `INotifyPropertyChanged` in WPF**

* **Purpose:** Notify the UI when a property value changes (supports **data binding**).
* Interface contains `PropertyChanged` event.

**Example:**

```csharp
public class Person : INotifyPropertyChanged {
    private string name;
    public string Name {
        get => name;
        set {
            name = value;
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs("Name"));
        }
    }
    public event PropertyChangedEventHandler PropertyChanged;
}
```

---

### **26) What is DataContext**

* `DataContext` is the **data source** for WPF bindings.
* Example:

```xaml
<Window DataContext="{Binding Source={StaticResource PersonVM}}">
    <TextBox Text="{Binding Name}" />
</Window>
```

* Connects **ViewModel** to **View**.

---

### **27) What is DataTrigger**

* **DataTrigger:** Changes UI properties **based on data conditions**.
* Example:

```xaml
<TextBlock Text="Status">
    <TextBlock.Style>
        <Style TargetType="TextBlock">
            <Style.Triggers>
                <DataTrigger Binding="{Binding IsActive}" Value="True">
                    <Setter Property="Foreground" Value="Green"/>
                </DataTrigger>
            </Style.Triggers>
        </Style>
    </TextBlock.Style>
</TextBlock>
```

---

### **28) Difference between IEnumerable & IQueryable**

| Feature     | IEnumerable                   | IQueryable                 |
| ----------- | ----------------------------- | -------------------------- |
| Namespace   | System.Collections            | System.Linq                |
| Execution   | In-memory (LINQ to Objects)   | Remote (LINQ to SQL/EF)    |
| Queryable   | Cannot translate query to SQL | Can translate query to SQL |
| Performance | Fetches all data              | Fetches only filtered data |

---

### **29) What is Binding & Its Types**

* **Binding:** Connect UI elements to data source.
* **Types:**

  1. **One-way:** UI updates when source changes
  2. **Two-way:** UI updates source and vice versa
  3. **One-time:** Binds only once
  4. **One-way-to-source:** Updates source, not UI

---

### **30) Difference between `ref` & `out`**

| Feature        | ref                                | out                              |
| -------------- | ---------------------------------- | -------------------------------- |
| Initialization | Must be initialized before passing | No need to initialize            |
| Purpose        | Pass by reference                  | Pass by reference & return value |
| Example        | `void Demo(ref int x)`             | `void Demo(out int x)`           |

---

### **31) Explain Overriding with Example**

* **Overriding:** Child class **redefines base class method** using `override`.

```csharp
class Base { public virtual void Show() => Console.WriteLine("Base"); }
class Child : Base { public override void Show() => Console.WriteLine("Child"); }

Base obj = new Child();
obj.Show(); // Child
```

---

### **32) What is Virtual Method**

* **Virtual Method:** Base class method that **can be overridden** in derived class.

```csharp
class Base { public virtual void Display() { Console.WriteLine("Base"); } }
```

---

### **33) What is Method Hiding**

* **Method Hiding:** Derived class **hides base class method** using `new` keyword.

```csharp
class Base { public void Show() => Console.WriteLine("Base"); }
class Child : Base { public new void Show() => Console.WriteLine("Child"); }

Base obj = new Child();
obj.Show(); // Base
```

* Difference: **Overriding** uses runtime polymorphism, **Hiding** uses compile-time binding.

---

Sure, Brijesh! Let’s go **deep dive** into your next set of .NET, SQL, and WPF topics with explanations, examples, and comparisons where needed.

---

### **34) What is Static Class**

* **Static Class:** A class that **cannot be instantiated** and **contains only static members**.
* **Purpose:** Utility/helper methods, constants.
* **Rules:**

  1. Cannot create object using `new`.
  2. All members must be `static`.
  3. Cannot have instance constructors.

**Example:**

```csharp
public static class Utils {
    public static int Add(int a, int b) => a + b;
}
int sum = Utils.Add(5, 10);
```

---

### **35) What is Constructor & Its Types**

* **Constructor:** Special method invoked **when object is created**.
* **Types:**

1. **Default constructor:** No parameters
2. **Parameterized constructor:** Accepts parameters
3. **Static constructor:** Initializes static members, called **once**
4. **Private constructor:** Used in Singleton pattern

**Example:**

```csharp
class Demo {
    public Demo() { Console.WriteLine("Default"); }
    public Demo(int x) { Console.WriteLine(x); }
    static Demo() { Console.WriteLine("Static"); }
}
```

---

### **36) Explain Joins in SQL**

* Joins combine rows from **two or more tables** based on a related column.

1. **INNER JOIN:** Only matching rows
2. **LEFT JOIN (LEFT OUTER):** All rows from left, matched rows from right
3. **RIGHT JOIN (RIGHT OUTER):** All rows from right, matched rows from left
4. **FULL OUTER JOIN:** All rows from both tables
5. **CROSS JOIN:** Cartesian product

**Example:**

```sql
SELECT e.Name, d.DeptName
FROM Employee e
INNER JOIN Department d ON e.DeptId = d.DeptId;
```

---

### **37) What is View in SQL**

* **View:** Virtual table derived from **SELECT query**.
* **Purpose:** Simplify queries, hide complexity, improve security.
* **Example:**

```sql
CREATE VIEW EmployeeView AS
SELECT Name, DeptId FROM Employee;
```

---

### **38) What are Constraints in SQL**

* **Constraints:** Rules applied to table columns to ensure **data integrity**.
* Types:

1. **PRIMARY KEY** – Unique & Not Null
2. **UNIQUE** – Unique values
3. **FOREIGN KEY** – Referential integrity
4. **CHECK** – Validates data
5. **DEFAULT** – Default value

---

### **39) Difference: Primary Key vs Unique Key**

| Feature            | Primary Key          | Unique Key                     |
| ------------------ | -------------------- | ------------------------------ |
| Null Allowed       | No                   | Yes (SQL Server allows 1 NULL) |
| Unique             | Yes                  | Yes                            |
| Multiple per Table | Only 1               | Multiple                       |
| Index              | Clustered by default | Non-clustered by default       |

---

### **40) Difference: Function vs Stored Procedure**

| Feature      | Function              | Stored Procedure |
| ------------ | --------------------- | ---------------- |
| Returns      | Single value or table | None or multiple |
| Execution    | Part of query         | `EXEC` command   |
| Side Effects | Cannot modify DB      | Can modify DB    |
| Parameters   | Limited               | Flexible         |

---

### **41) How to Optimize a Query**

* Use **Indexes**
* Avoid `SELECT *`
* Use **joins instead of subqueries**
* Filter early (`WHERE`)
* Avoid functions on columns in WHERE
* Use **Stored Procedures**
* Analyze **execution plan**

---

### **42) What are Indexes**

* **Index:** Improves **query performance** by allowing faster searches.
* Types: **Clustered** and **Non-clustered**.
* **Clustered index:** Data stored in index order (one per table).
* **Non-clustered index:** Separate structure, multiple allowed.

---

### **43) What is a Cursor**

* **Cursor:** Database object to **iterate row by row**.
* Types: **Static, Dynamic, Forward-only, Keyset**
* Generally **avoid** cursors; prefer set-based operations.

**Example:**

```sql
DECLARE emp_cursor CURSOR FOR SELECT Name FROM Employee;
OPEN emp_cursor;
FETCH NEXT FROM emp_cursor INTO @name;
```

---

### **44) Types of Indexing**

1. **Clustered Index** – Data physically sorted
2. **Non-Clustered Index** – Separate structure
3. **Unique Index** – Ensures uniqueness
4. **Composite Index** – Index on multiple columns
5. **Full-Text Index** – Search text fields efficiently

---

### **45) Difference `throw` vs `throw ex`**

| Feature     | throw                            | throw ex                            |
| ----------- | -------------------------------- | ----------------------------------- |
| Stack Trace | Preserves original               | Resets stack trace                  |
| Use         | Rethrow exception                | Throw new or existing exception     |
| Example     | `catch(Exception ex) { throw; }` | `catch(Exception ex) { throw ex; }` |

* **Best practice:** Use `throw` to preserve stack trace.

---

### **46) What is Exception Handling**

* Mechanism to handle **runtime errors** gracefully.
* Keywords: `try`, `catch`, `finally`, `throw`
* Example:

```csharp
try { int x = 5/0; }
catch(DivideByZeroException ex) { Console.WriteLine(ex.Message); }
finally { Console.WriteLine("Cleanup"); }
```

---

### **47) What is `IDisposable` Interface**

* **IDisposable:** Provides `Dispose()` method to **release unmanaged resources**.
* Example:

```csharp
class FileResource : IDisposable {
    public void Dispose() { /* close file */ }
}
using(var file = new FileResource()) { /* work */ }
```

---

### **48) What is `ICommand` Interface**

* Used in **MVVM** for **binding actions** (like button click) to **ViewModel**.
* Members: `Execute()`, `CanExecute()`, `CanExecuteChanged`
* Example:

```csharp
public class RelayCommand : ICommand {
    public event EventHandler CanExecuteChanged;
    public bool CanExecute(object parameter) => true;
    public void Execute(object parameter) { /* action */ }
}
```

---

### **49) Difference: Task vs Thread**

| Feature      | Thread                     | Task                                |
| ------------ | -------------------------- | ----------------------------------- |
| Abstraction  | Low-level                  | High-level                          |
| Creation     | Thread t = new Thread(...) | Task.Run(() => ...)                 |
| Return Value | None                       | Can return value (`Task<T>`)        |
| Management   | Manual                     | Automatic scheduling via ThreadPool |

---

### **50) What is Relay Command**

* **RelayCommand:** Implementation of `ICommand` used in **MVVM**.
* Allows **binding buttons to ViewModel methods** without code-behind.

**Example:**

```csharp
public ICommand SaveCommand => new RelayCommand(param => SaveData());
```

---

### **51) What is Virtualization in WPF**

* **Virtualization:** Only creates **UI elements for visible items** in controls like `ListBox`, `DataGrid`.
* Improves **performance** with **large collections**.
* Implemented via `VirtualizingStackPanel`.

**Example:**

```xaml
<ListBox ItemsSource="{Binding Items}" VirtualizingStackPanel.IsVirtualizing="True"/>
```

---

