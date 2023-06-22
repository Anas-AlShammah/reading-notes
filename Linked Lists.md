#Linked Lists

## Big O

the efficiency is evaluated based on 2 factors:

1- Running Time

2- Memory Space

we describe the Worst Case of efficiency

Consider 4 Key Areas for analysis :

1- Input Size

2- Units of Measurement 

3- Orders of Growth

4- Best Case ,Worst Case , Average Case 

### Input Size

the size of each parameter value and the number of parameters

use letter n to refer to the Input Size value

### Units of Measurement 

we consider three measurements of time:

1- The time in milliseconds from the start of a function execution until it ends

2- The number of operations that are executed

3- The number of “Basic Operations” that are executed

In order to quantify Memory Space, we can consider Four Sources of Memory Usage during function run-time:

1- The amount of space needed to hold the code for the algorithm.

2- The amount of space needed to hold the input data.

3- The amount of space needed for the output data.

4- The amount of space needed to hold working space during the calculation

### Orders of Growth

![Orders Of Growth](OrdersOfGrowth.png)

Constant Complexity means that no matter what inputs are thrown at our algorithm, it always uses the same amount of time or space. The number 1 is used to represent a constant value. The actual number of units will most likely be greater than 1, we round this number down to 1 to represent our estimate of complexity that is independant of n.
This algorithm has an O(1) constant efficiency, no matter the size of a or b, this function simply returns the sum of those 2 numbers.

ALGORITHM Sum(number a, number b)

   number val <-- a + b
   return val


   ## Linked List

   A Linked List is a sequence of Nodes that are connected/linked to each other. The most defining feature of a Linked List is that each Node references the next Node in the link.

   There are two types of Linked List - Singly and Doubly. 

   ### Single Linked List:Navigation is forward only
   Data & Link
   ### Doubly Linked List:
   Link & Data & Link 
   Terminology:
Linked List - A data structure that contains nodes that links/points to the next node in the list.
Singly - Singly refers to the number of references the node has. A Singly linked list means that there is only one reference, and the reference points to the Next node in a linked list.
Doubly - Doubly refers to there being two (double) references within the node. A Doubly linked list means that there is a reference to both the Next and Previous node.
Node - Nodes are the individual items/links that live in a linked list. Each node contains the data for each link.
Next - Each node contains a property called Next. This property contains the reference to the next node.
Head - The Head is a reference of type Node to the first node in a linked list.
Current - The Current is a reference of type Node to the node that is currently being looked at. When traversing, you create a new Current variable at the Head to guarantee you are starting from the beginning of the linked list.