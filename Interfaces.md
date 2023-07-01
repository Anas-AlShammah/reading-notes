# Interface

An interface defines a contract.

An interface is an abstraction that indicates what a class that implements it can do. An interface contains functionalities that a class can implement. 

- An interface can contain methods or properties but not fields, constants, or constructors.


Incorrect
``` C#
public interface IWorker
{
    string Name;    // No - Fields forbidden
    const int Age;  // No - Constants forbidden
    IWorker();      // No - Constructors forbidden
}
```
Correct
``` C#
public interface IWorker
{
    string Name { get; }
    void DoWork();
}
```
- A class can inherit from multiple interfaces, but only from one class. To derive from several interfaces, list them separated by a comma


Incorrect
```c#
public class Worker
{
    public virtual void DoWork()
    {
        // Some code
    }

    public virtual void PrintResult()
    {
        // Some code
    }
}

public class Person
{
    public virtual string GetName()
    {
        // Some code
    }
}

// Wrong! Con't derive from two classes
public class HumanWorker : Worker, Person
{
    // Some code
}

```
Correct
```c#

public interface IWorker
{
    void DoWork();
    void PrintResult();
}

public interface IPerson
{
    string GetName();
}

// This is OK: derive from two interfaces
public class Worker : IWorker, IPerson
{
    public void DoWork()
    {
        // Some code
    }

    public void PrintResult()
    {
        // Some code
    }

    public string GetName()
    {
        // Some code
    }
}
```

- If a class implements an interface, it must implement all of its members.

- Interface members are automatically public , and they can't include any access modifiers.

Incorrect

```csharp
public interface IWorker
{
    string Name { get; }
    void DoWork();
}

public class Worker : IWorker
{
    // Doesn't implement interface
    private void DoWork()   // Wrong
    {
    }

    // Doesn't implement interface
    protected string Name { get; }  // Wrong
}
```

Correct

```csharp
public interface IWorker
{
    string Name { get; }
    void DoWork();
}

public class Worker : IWorker
{
    // Public method implements interface
    public void DoWork()   // Right
    {
    }

    // Public property implements interface
    public string Name { get; }  // Right
}
```
- An interface can't have implementation of methods; only declaration.

