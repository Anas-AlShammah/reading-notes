# Collections & Enums

## Collections

A Collection is a class

```csharp
Car<string> list = new Car<string>();
```
## Generics vs. Non-Generics
- Generics
- List<T>
- Dictionary<T>
- SortedList<T>
- Queue<T>
- IEnumerable<T>
- IList<T>
- Collection<T>
- LinkedList<T>

Non-Generics
are not really used much anymore

ArrayList

HashTable

SortedList

Queue

Stack

IEnumerable

ICollection

---

can use a foreach loop to traverse through a collection

add values directly to a collection upon instantiation, use a collection initializer

```csharp
Car<string> list = new Car<string>{"BMW","Kia"};
```

## Enums
Enums, short for enumeration types, are a feature in programming languages that allow you to define a named set of related named values. An enum provides a way to define a set of constants, typically represented as integral values, that can be assigned to variables.

Enums are useful when you have a fixed set of values that a variable can take, such as days of the week, months of the year, or states of an object. Instead of using plain integers or strings to represent these values, enums provide a more structured and self-descriptive approach.

```csharp
enum Days
{
   Sunday,
   Monday,
   Tuesday,
   Wednesday,
   Thursday,
   Friday,
   Saturday
}

```

Enums can also have an underlying type specified explicitly. By default, the underlying type is int, but you can specify an alternative integral type such as byte, short, or long using a colon (:) followed by the desired type.

``` csharp
enum Months : byte
{
   Jan,
   Feb,
   Mar,
   Apr,
   May,
   Jun,
   Jul,
   Aug,
   Sep,
   Oct,
   Nov,
   Dec
}

```
Using enums, we can assign enum values to variables, 
compare them, perform arithmetic operations,
and use them in switch statements to handle different cases based on the enum value
