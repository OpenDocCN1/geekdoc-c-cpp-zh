
## Basic Concepts

**Chapter Objective**

- Describe the abstract data type
- Usage of abstract data type
- Define the algorithm
- Characteristics of algorithm
- Types of algorithm
- Measuring the complexity of an algorithm.

### 1.1 INTRODUCTION

Data structure is widely used in several domains of computer science. With the advancement in computer electronics, processing speed and memory are no longer constraints for the computer system. Still, for massive data processing, efficient program plays a significant role in generating instant results. Therefore, it is significant that the algorithm employed should be efficient at the same time should require minimum time and space for execution.

It is equally important that the program serving one objective should solve other similar objective without undergoing major modifications. During the program implementation, underlying complexity should remain hidden from the user. To deal with all the aforementioned objectives, this chapter highlights the various aspects of algorithm that have significant impact on the performance of a program.

### 1.2 ABSTRACT DATA TYPE (ADT)

In a language, data types play a significant role in the representation of data. ADT can be defined as a mathematical representation that governs the various factors including:

- Type of information accepted.
- Range of permitted values.
- Memory space needed.
- Operations permitted on the data type.

Primitive data type includes integer, real, character etc. on such data types, only basic operations such as addition, subtraction, multiplication etc. are allowed. Consequently, complex operations cannot be applied on primitive data types. This limitation has been overcome with the help of ADT as it needs to define the complex operations.

In abstract data type (ADT), users are provided with the limited details which are really needed to them; remaining information remains hidden and inaccessible to the users. Hiding implementation details from the user serve the wide purposes. For instance, modification in the code may be needed due to bugs or any other reasons. With the usage of ADT, only hidden details are changed without affecting the user level accessibility. Hence, user is not affected due to the modification or any inclusion of additional functionality.

Object oriented language has the capability to support the abstract data type. In object oriented language, complex as well as additional operations are required to be defined. ADT facilitates in defining additional operations that were not possible on primitive data types. Even the hiding of internal details is widely supported in the object oriented language. In object oriented approach, to hide the members, they are declared as private. In complex program, usage of friend function is not allowed since it allows the accessibility of private member. ADT offers flexibility to implement the definition for complex structure, although it might have implemented for primitive data type.

### 1.2.1 Need of an ADT

User needs to implement the abstract data types due to the variety of reasons. This is facilitated with the help of interface that is offered by the implementer. Abstract data type needs to implement various details. As a pre-requisite, code offered should be reliable and robust. Reliability can be attained with the help of data hiding. Consequently, user doesn’t enjoy the flexibility to access the defined variable.

### 1.2.2 Implementation of an ADT

Even though, ADT is widely used due to the existence of its various promising features. However, before implementation, readers need to learn many of the significant terms and their meaning associated. Same has been defined herein:

**Constructor/Modificators -** In a language, constructor is a special method that is capable to build or change the state of an object. Name of the constructor cannot be assigned arbitrarily instead; its name is governed by the class name for which constructor is to be created. Constructor name is same as the class name. Constructors are invoked implicitly by their objects when they are created.

**Accessors -** Methods that can be accessed with the help of an object are known as accessors. Values to the variable can be assigned with the help of accessors. Consider a case of a queue implementation; an accessor can be developed to carry out the various operations needed. For instance, insertion of items in a queue is termed as en-queue whereas removal of item is known as de-queue (Readers who are not aware of the queue, please refer section 6.1, basic definitions, for clarity of the topic). Correspondingly, enqueue and dequeue accessors can be implemented. Due to the usage of ADT, user does not need to know the implementation details. Instead, can concentrate on the usage of various functions offered by enqueue and dequeue accessors. In addition to the aforementioned operations, one more operation can be applied that does not move the item but lets us determine the item(s) that is available at the front of the queue without removing it.

During the implementation of ADT, we need to learn the various input, output and changes that can be caused due to the insertion of the items. Indeed, we need to determine the final output after the changes are incorporated. Same has been enumerated in table 1.1 by considering the case of a queue.

**Table 1.1: Queue interface**

| Name | Description | Input | Output | Changes |
|---|---|---|---|---|
| Enqueue | Places an item at the end of a queue, if queue is not full | Queue and an item | Integer value | Upon addition of an Item, rear will move one position backwards |
| Dequeue | Removes an item from the front of the queue, if queue is not empty | Queue | Integer value | Front item is removed and the front will point to the next element |
| Empty | Examines whether the queue is empty or not | Queue | A Boolean value |  |
| Item | Returns the first element without making any changes at front | Queue | Front of the queue |  |

Axioms - Axioms are the mathematical representation of the various operations that can be carried out by utilizing ADT. Consider a case, if the queue is q1 and the item to be inserted is 'e' then the axioms are:

- Enqueue(q1,e)=e //Element inserted
- Dequeue ( Enqueue(q1,e))=e    //Element removed
- Empty (Enqueue(q1,e))=Boolean  //status flag
- Item(Enqueue(q1,e))=e    //first element of queue

Once the axioms have been written, they lay the fertile ground to denote the prototype of the functions that can be used to accomplish a specific task. Prototype of the above axioms can be the following:

```
Template<class T>
T enqueue (Q q, T t1); //insert the items in the queue.
T dequeue (Q q); //returns the item removed.
bool Empty (Q);   // To check whether the queue is empty
T Q (T item);      // to determine the first element of the queue
```

Above functions signify that the usage of an ADT makes the programmer's life easy. Any error or complexity can be analyzed well before time. Correspondingly, it saves a lot of time during the testing stage.

### 1.3 ALGORITHM

In computers, we need to solve wide variety of existing problems, majority of them fall under the category of simple or complex. Any problem can be solved by applying sequence of statements. Algorithms are comprising the set of statements needed to solve a given problem.

Algorithm - In majority of the cases, algorithms are written using pseudo code. Coder or developer will translate pseudo code used in the algorithm into a specific code of the target programming language. Good algorithm is a pre-requisite for good functions. To overcome a problem, sequential set of statements are grouped together, and may be categorized into simple statements, conditional statements, loops statements etc. It requires careful thought for writing an efficient and cost effective code by utilizing these language constructs. For instance, the written logic should not allow a loop to continue, once search is already accomplished. If the element is already found then the looping statement must terminate. A faulty algorithm to search an element has been discussed as follows:

```
Write an algorithm to search an item in a given array
int search (a [], element)
{
found=false;
k=0;
while (not end of a)
{
if (a[k] == element)
{
found=true;
} // end of if
increment k;
}// end of while
}// end of search
```

In the above algorithm, even though the element has been found at its first location, despite that searching will continue till the end of an array is reached. However, it is undesired; since the loop is allowed to execute without any objective. Consequently, we have wasted the precious processor cycle without any aim. In order to gain high degree of efficiency, the above code needs to be modified in a manner so that any possible unnecessary cycle of loop can be eliminated. Same has been described in the following program.
