
# Data Structures and Algorithms

## Why Does This Topic Matter?

One of the most important things to consider when choosing a data structure is the type of data that we need to store. For example, if we need to store a list of items in a specific order, we would use a sorted array. If we need to store a list of items that can be inserted or deleted in any order, we would use a linked list.

Another important factor to consider is the amount of data that we need to store. If we only need to store a small amount of data, we can use a simple data structure such as an array. However, if we need to store a large amount of data, we will need to use a more complex data structure such as a tree or a graph.

Finally, we also need to consider the performance of the data structure. Some data structures are more efficient than others for certain operations. For example, binary search is a very efficient way to search for an item in a sorted array. However, binary search cannot be used to insert or delete items from an array.

## what we are studying in this module?
commonly used data structures every programmer must know.
### Recursion
#### Base Case
when the function doesn't call itself again.
#### Recursive Case 
when function calls itself.
How can we ensure that we’ll avoid an infinite recursive call stack?

There are two ways to avoid an infinite recursive call stack:

Base case: A base case is a condition that stops the recursion. For example, if you are writing a recursive function to find the factorial of a number, the base case would be when the number is 0. In this case, the function would return 1.
Maximum recursion depth: You can also set a maximum recursion depth. This is the maximum number of times that the function can be called recursively before it stops.
It is important to note that recursion can be a very powerful tool, but it can also be dangerous if it is not used correctly. It is important to understand the risks of recursion and to take steps to avoid infinite recursion.
### Big-O
is the way how we measure how good a data structue is doing a specifc thing

like adding,sorting,searching

### 1. Arrays
An array is a structure of fixed-size, which can hold items of the same data type.

array is quite literally a continuous block of cells in the computer memory by keeping track of its memory location 
really good at retrieving items 
in lower-level languages we have to declare the size of our array in advance okey
### 2. Linked Lists
the atomic unit of the linked list is node 
which contains a value and a pointer (connect us to the next node in the chain )
first node named the head
last node named the tail
good at adding new nodes
and deleting nodes 
not good at retrieval and searching 
### 3. Stacks & Queues
the stacks  is a blast in last in first out 
when add item to top it's called pushing and then we pop off the top
super important with algorithm called depth-first search 

the Queues is first in first out 
like any hue or line 
adding item to the end is called queueing
and remove it from the front is dequeue
used for important algorithm called breadth-first search 
but have limited use cases 
### 4. Hash Tables
A Hash Table is a data structure that stores values which have keys associated with each of them.

two keys could hash to the sane memory loction (collisoin)
good at both add and retrieving 
not good at the collisions
### 5. Graphs & Trees
A graph consists of a finite set of vertices or nodes and a set of edges connecting these vertices.

The order of a graph is the number of vertices in the graph. The size of a graph is the number of edges in the graph.

Two nodes are said to be adjacent if they are connected to each other by the same edge.

A tree is a hierarchical structure where data is organized hierarchically and are linked together. This structure is different from a linked list whereas, in a linked list, items are linked in a linear order.

## Things I Want to Know More About

- How do different data structures and algorithms impact the performance of an application?
- What are some real-life


