
### 3.2.1 Primitive Operations

The three basic stack operations are push, pop, and getTop. Besides these, there are some more operations that can be implemented on a stack such as stack_initialization, stack_empty, and stack_full. The stack_initialization operation prepares the stack for use and sets it to a vacant state. The stack_empty operation simply tests whether the stack is empty. The stack_empty is useful as a safeguard against an attempt to pop an element from an empty stack. Popping an empty stack is an error condition. The stack_empty condition is also termed stack underflow. In ideal conditions, stacks should possess infinite capacity so that the subsequent elements can always be pushed, regardless of the number of elements already present on the stack. However, computers always have finite memory capacity, and we do need to check the stack_full condition before doing push because pushing an element in a full stack is also an error condition. Such a stack full condition is called stack overflow.

Another stack operation is getTop. This returns the top element of the stack without actually popping it. A few more stack operations include traversing the stack, counting the total number of elements in the stack, and copying the stack.

Let us quickly recall all the stack operations:

- 1. Push—inserts an element on the top of the stack
- 2. Pop—deletes an element from the top of the stack
- 3. getTop—reads (only reading, not deleting) an element from the top of the stack
- 4. Stack_initialization—sets up the stack in an empty condition
- 5. Empty—checks whether the stack is empty
- 6. Full—checks whether the stack is full

### Push

The push operation inserts an element on the top of the stack. The recently added element is always at the top of the stack. Before every push, we must ensure whether there is a room for a new element (Fig. 3.3).

![](img/a99ec79093c067f0bed8f1086197950e_108_0.png)

Fig. 3.3 The push operation

When there is no space to accommodate the new element on the stack, the stack is said to be full (Fig. 3.4). If the operation push is performed when the stack is full, it is said to be in overflow state, that is, no element can be added when the stack is full. The push operation modifies the top since the newly inserted element becomes the topmost element (Fig. 3.3).

![](img/a99ec79093c067f0bed8f1086197950e_109_0.png)

Fig. 3.4 The stack full condition (stack capacity = 3)

### Pop

The pop operation deletes an element from the top of the stack and returns the same to the user. It modifies the stack so that the next element becomes the top element (Fig. 3.5).

![](img/a99ec79093c067f0bed8f1086197950e_109_1.png)

Fig. 3.5 The pop operation

When there is no element available on the stack, the stack is said to be empty. If pop is performed when the stack is empty, then the stack is said to be in an underflow state (Fig. 3.6).

![](img/a99ec79093c067f0bed8f1086197950e_109_2.png)

Fig. 3.6 The empty stack

The pop operation should not be performed when the stack is empty, and hence before every pop, we must ensure that the stack is not empty. After deleting the last element from the stack, the stack should be set to an empty state.

### GetTop

The getTop operation gives information about the topmost element and returns the element on the top of the stack. In this operation, only a copy of the element, which is at the top of the stack, is returned. Hence, the top is still set to the same element (Fig. 3.7).

![](img/a99ec79093c067f0bed8f1086197950e_110_0.png)

Fig. 3.7 The getTop operation

This is the key difference between the pop and getTop operations. The getTop operation does not modify the variable top. It signals the stack underflow error if the stack is empty.

As both insert and delete operations are allowed only at one end of the stack, it retrieves data in the reverse order in which the data is stored. In Fig. 3.8, let S = {A, B, C}.

![](img/a99ec79093c067f0bed8f1086197950e_110_1.png)

Fig. 3.8 Stack and push operations

Suppose that the order of the operations is push(A), push(B), and then push(C). When we remove these elements out of the stack, they will be removed in the order C, B, and then A. This is shown in Fig. 3.9.

![](img/a99ec79093c067f0bed8f1086197950e_111_0.png)

Fig. 3.9 Stack and pop operations

Elements are taken out in the reverse order of the insertion sequence. So a stack is often called last in first out (LIFO) or first in last out (FILO) data structure.

## 3.3 STACK ABSTRACT DATA TYPE

Let us now see the data object, operations, and axioms associated with the stack. Any sets of elements that are of the same data type can be used as a data object for stacks. The meaning of ‘same data type’ is that all the elements in the stack should be of the same nature, having common representational logical properties. For example, stack of integers, stack of names of students, stack of employee records, and stack of records of processes of the operating system.

The following five functions comprise a functional definition of a stack:

- 1. Create(S)—creates an empty stack
- 2. Push(i, S)—inserts the element i on the stack S and returns the modified stack
- 3. Pop(S)—removes the topmost element from the stack S and returns the modified stack
- 4. GetTop(S)—returns the topmost element of stack S
- 5. Is_Empty(S)—returns true if S is empty, otherwise returns false

However, when we choose to represent a stack, it must be possible to build these operations. Before we do this, let us describe formally the structure stack.

```
ADT Stack(element)
1. Declare Create() → stack
2. push(element, stack) → stack
3. pop(stack) → stack
4. getTop(stack) → element
5. Is_Empty(stack) → Boolean;
6. for all S ∈ stack, e ∈ element, Let
7. Is_Empty(Create) = true
8. Is_Empty(push(e, S)) = false
9. pop(Create()) = error
10. pop(push(e, S)) = S
11. getTop(Create()) = error
12. getTop(push(e, S)) = e
13. end
14. end stack
```

The five functions with their domains and ranges are declared in lines 1 through 5. Lines 6 through 13 are the set of axioms that describe how the functions are related. Lines 10 and 12 are important because they define the LIFO behaviour of the stack. This description shows an infinite stack of no upper bound or roof on the number of elements specified. This will be discussed when we represent this structure using C++.

We studied the concept of ADT in Chapter 1. The ADT stack is defined in Section 3.3. To implement the ADT stack in C++, the operations are often implemented as functions to provide data abstraction. A program that uses stacks would access the stacks only through these functions and would not be concerned about the implementation.

## 3.4 REPRESENTATION OF STACKS USING SEQUENTIAL ORGANIZATION (ARRAYS)

A stack can be implemented using both a static data structure (array) and a dynamic data structure (linked list). The simplest way to represent a stack is by using a one-dimensional array. A stack implemented using an array is also called a *contiguous stack*.

An array is used to store an ordered list of elements. A stack is an ordered collection of elements. Hence, it would be very simple to manage a stack when represented using an array. The only difficulty with an array is its static memory allocation. Once declared, the size cannot be modified during run-time. We have already read that this leads to either poor utilization of the space or inability to accommodate all possible data elements. This is because we declare an array to be of arbitrarily maximum size before compilation.

Figure 3.10 shows the realization of a stack using arrays.

![](img/a99ec79093c067f0bed8f1086197950e_112_0.png)

Fig. 3.10 Stack using array

Let Stack[n] be a one-dimensional array. When the stack is implemented using arrays, one of the two sides of the array can be considered as the top (upper) side and the other as the bottom (lower) side as in Fig. 3.10.

Let us discuss the top side, which is most commonly used. The elements are stored in the stack from the first location onwards. The first element is stored at the 0th location of the array Stack, which means at Stack[0], the second element at Stack[1], the i-th element at Stack(i - 1), and the n-th element at Stack(n - 1). Associated with the array will be an integer variable, top, which points to the top element in the stack. The initial value of top is -1 when the stack is empty. It can hold the elements from index 0, and can grow to a maximum of n - 1 as this is a static stack using arrays.

Program Code 3.1 gives the definition of class Stack and lists the function prototypes for a set of basic operations.

![](img/a99ec79093c067f0bed8f1086197950e_113_0.png)

The simplest way to implement an ADT stack is using arrays. We initialize the variable top to -1 using a constructor to denote an empty stack. The bottom element is represented using the 0th position, that is, the first element of the array. The next element is stored at the 1st position and so on. The variable top indicates the current element at the top of the stack.
