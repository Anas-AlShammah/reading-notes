# Classes & Memory Management

## Object-Oriented Programming

Object-oriented programming mimics real-world objects in code. In C#, everything is essentially a class, and we can instantiate objects from classes that we can manage at a smaller level.

## Class vs Object

### What are Classes?

A class is a blueprint for a specific type or category of object. It outlines the properties, methods, and general behavior that each object of that class will have.

### Object:

To create an object, we use the `new` keyword. Objects based on classes are referred to by reference, making classes known as reference types. 

## What do we mean by static?

If something is marked as static, it means that it belongs to the class as a whole, not to individual objects. It is shared across all instances of the class. If you change something in the class that is static, it will affect all instances of the class.

## Constructors

- How many constructors should/can I have?
- What is a default constructor?

A constructor is defined like a method, except that the method name and return type are reduced to the name of the enclosing type. Constructors enable the programmer to set default values, limit instantiation, and write flexible and easy-to-read code.

### Default Constructors

If you don't provide a constructor, one is automatically generated for you. This default constructor sets the member variables to their default values.

- Object initializers: `var newObject = new ObjectName { propertyName = "value" }` or `newObject.propertyName = "value"`
- Properties, backing fields, auto-implemented properties

Properties look like fields from the outside, but internally they contain logic, similar to methods. They can be read-write (both get and set accessors), read-only (only get accessor), or write-only (only set accessor). Write-only properties are rare and are commonly used to restrict access to sensitive data.

A backing field is a private field used by properties when you want to modify or use private field data. In other words, a property is just a reference to another private variable.

Example:

```csharp
private string name;  // the name field (called a 'backing store' note how it is private)

public class Date
{
    private int month = 7;  // Backing store

    public int Month
    {
        get
        {
            return month;
        }
        set
        {
            if ((value > 0) && (value < 13))
            {
                month = value;
            }
        }
    }
}

class Employee
{
    private string name;
    
    public string Name
    {
        get
        {
            return name != null ? name : "NA";
        }
    }
}
```
## Garbage Collection

When you declare a variable in a .NET application, it allocates some chunk of memory in the RAM. This memory has three things:

- **Name of the variable**
- **Data type of the variable**
- **Value of the variable**

---

## Value vs Reference Type

### Value Types

A value type is a data type that holds the data within its own memory allocation. Examples include `int`, `float`, `double`, `long`, enums, and structs. Here are some characteristics of value types:

- Value types only live on the stack.
- Value types are created at compile time and stored in stack memory. The garbage collector (GC) cannot access the stack.
- Value types are copied when assigned or passed as method arguments, and manipulating the copy does not affect the original value.

### Reference Types

A reference type is a data type that contains a reference (address) to the object rather than the object itself. Common reference types include strings, objects, classes, arrays, indexers, and interfaces. Consider the following aspects of reference types:

- Reference type variables are stored in the heap.
- When assigning a reference variable to another, it creates a second reference pointing to the same location on the heap.
- Reference types rely on the garbage collector (GC) for memory management.
- Reference types can be randomly accessed and have no dependencies on one another.

#### Example/Analogy

**Stack vs Heap**

- **Value Types**
  - Created at compile time and stored in stack memory. The GC cannot access the stack.

- **Reference Types**
  - Reference type variables are stored in the heap.

**Stack**

Imagine it like a stack of shoe boxes. The stack keeps track of what is being executed in the code. Here are some characteristics of the stack:

- Variables allocated to the stack are stored directly in memory, enabling fast access.
- The stack is allocated at compile time and holds value types.
- It is self-maintaining and takes care of its own memory management.
- The stack uses static memory allocation.

**Heap**

The heap is responsible for dynamic memory allocation. It allocates memory at runtime and holds objects, reference types, and sometimes value types. Consider the following aspects of the heap:

- Accessing data on the heap is relatively slower than on the stack.
- The heap size is only limited by the size of virtual memory.
- The heap relies on the garbage collector (GC) for memory management.
- Reference types usually go to the heap.

You can use the stack if you know exactly how much data you need to allocate before compile time and if it is not too large. On the other hand, you can use the heap if you don't know the exact amount of data needed at runtime or if you need to allocate a significant amount of data.

---

