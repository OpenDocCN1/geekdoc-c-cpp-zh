
![](img/a99ec79093c067f0bed8f1086197950e_281_0.png)

Fig. 6.71 Polynomial representation (a) The GLL for 9x^2y^2 + 6xy^2 + y + x^2 (b) The GLL with three fields, omitting unused field

![](img/a99ec79093c067f0bed8f1086197950e_281_1.png)

Fig. 6.72 The GLL for 8x^3y^2z^2 + 3x^3y^2z^2 + y^2z^2 + xy^2z^2 + 8x + 9y

## 6.13.4 Representation of Sets Using Generalized Linked List

Let A be a set, A = {a, b, {c, d, { }}, {e,f}, g}. Here, A consists of elements that are either atoms or sets. Hence, we need a GLL node to convey whether the member of set is an atom or a set. The generalized list can be represented using the node structure as Fig. 6.73.

| Tag | Data/dLink | nLink |
|---|---|---|

Fig. 6.73 Generalized list representation using node structure

Here, the tag field is set to 0 if the member is an atom and is set to 1 if it is another list. Accordingly, the second field would represent the data or downlink, respectively.

Figure 6.74 shows the GLL representation for the following sets:

- B = (a, b, c), d)
- C = (B, B, ())
- D = (a, D)

Figure 6.75 shows the GLL representation for the set A = { {a, b}, {{c, d}, e} }.

![](img/a99ec79093c067f0bed8f1086197950e_282_0.png)

Fig. 6.74 The GLL representation for B, C, and D

![](img/a99ec79093c067f0bed8f1086197950e_282_1.png)

Fig. 6.75 The GLL representation for A

The set X = {L, M, {N, {O, P}}, {Q, {R, {S, T}}, A, {B, C}} } is pictorially represented using a generalized linked list in Fig. 6.76.

![](img/a99ec79093c067f0bed8f1086197950e_283_0.png)

Fig. 6.76 The GLL for set X

We have represented the polynomials and sets using generalized linked list. Let us write the functions for traversing and printing the generalized linked list.

## Printing Generalized Linked Lists

Program Code 6.24 gives the code for printing a GLL.

```
PROGRAM CODE 6.24
void GLL :: PrintGLL()
{
    Stack S;
    GLLNode *curr = Null;
    S.Push(Head);
    curr = Head;
    while(1)
    {
        if(curr == Null)
        {
            if (!S.IsEmpty())
            {
                curr = S.Pop();
                if(curr->tag == 1)
                    cout << curr->data;
                curr = curr->mlink;
            }
            else if(curr->link != Null)
            {
                S.push(curr->mlink);
                curr = curr->link;
            }
        } //end if
    } //end while
} // end print
```

## 6.14 MORE ON LINKED LISTS

The function traversal of SLL can be used with a few modifications for polynomial evaluation. Given a value of x, we have to evaluate the polynomial as shown in Program Code 6.14.

## 6.14.1 Copying a Linked List

Consider the Copy_List( ) function, shown in Program Code 6.25, that takes a list and returns a complete copy of that list. One pointer can iterate over the original list in the usual way. Two other pointers can keep track of the new list: one head pointer and one tail pointer, which always points to the last node in the new list. The first node is done as a special case, and then the tail pointer is used in the standard way for the others.

```
PROGRAM CODE 6.25
Node *List :: CopyList()
{
 Node *current = Head;
 Node *newList = Null;
 Node *Tail = Null;
 while(current != Null)
 {
 if(newList == Null)
 {
 newList = new Node;
 newList->Data = current->Data;
 newList->link = Null;
 Tail = newList;
 }
 else
 {
 Tail->link = new Node;
 Tail = Tail->link;
 Tail->Data = current->Data;
 Tail->link = Null;
 }
 current = current->link;
 }
 return(newList);
}
```

## 6.14.2 Computing the Length of a Linked List

The Length( ) function, in Program Code 6.26, takes a linked list and computes the number of elements in the list.

Length() is a simple list function, but it demonstrates several concepts, which will be used later in more complex list functions.

```
PROGRAM CODE 6.26
int Llist :: Length()
{
    Node *current = Head;
    int count = 0;
    while(current != Null)
    {
        count++;
        current = current->link;
    }
    return count;
}
```

### Calling Length()

Program Code 6.27 is a typical code that calls Length(). It first calls create() to make a list and store the head pointer in a local variable. It then calls Length() on the list and catches the int result in local variable.

```
PROGRAM CODE 6.27
void LengthTest()
{
    Llist myList;
    myList.Create();
    int len = myList.Length();
}
```

## 6.14.3 Reversing Singly Linked List Without Temporary Storage

The procedure for reversing a singly linked list without temporary storage is illustrated by Program Code 6.28.

```
PROGRAM CODE 6.28
void Llist :: Reverse()
{
    Node *curr, *prev, *next;
    prev = Head;
    curr = Head->link;
    prev->link = Null;
    while(curr != Null)
    {
        next = curr->link;
        curr->link = prev;
        prev = curr;
        curr = next;
    }
    Head = prev;
}
```

## 6.14.4 Concatenating Two Linked Lists

Concatenation of two linked lists is illustrated by Program Code 6.29.

```
PROGRAM CODE 6.29
void Llist :: concatenate(Llist A)
{
    Node *X, *Y;
    X = Head;
    Y = A.Head;
    while(X->link != Null)
    {
        X = X->link;
    }
    X->link = Y;
    Head = X;
}
//A call to concatenate:
{
    Llist L1, L2;
    L1.Create(); L2.Create();
    L1.Concatenate(L2);
}
```

Here, X and Y are concatenated, and X is the pointer to the first node of the resultant list.

## 6.14.5 Erasing the Linked List

The procedure for erasing a linked list and returning all nodes to the free pool of memory is illustrated by Program Code 6.30.

```
PROGRAM CODE 6.30
void Llist :: ~Llist()
{
    Node *temp;
    while(Head != Null)
    {
        temp = Head;
        Head = Head->link;
        delete temp;
    }
}
```

## 6.15 APPLICATION OF LINKED LIST—GARBAGE COLLECTION

Memory is just an array of words. After a series of memory allocations and de-allocations, there are blocks of free memory scattered throughout the available heap space. To be able to reuse this memory, the memory allocator will usually link the freed blocks together in a free list by writing pointers to the next free block in the block itself. An external free list pointer points to the first block in the free list. When a new block of memory is requested, the allocator will generally scan the free list looking for a free block of suitable size and delete it from the free list (relinking the free list around the deleted block).

One of the components of an operating system is the memory management module. This module maintains a list, which consists of unused memory cells. This list very often requires the operations to be performed on the list, such as `insert`, `delete`, and `search` (traversal). Such a list implemented as a linked organization is called the *list of available space*, *free storage list*, or the *free pool*.

Suppose some memory block is freed by the program. The space available can be used for future use. One way to do so is to add the blocks in the free pool. For good memory utilization, the operating system periodically collects all the free blocks and inserts into the free pool. Any technique that does this collection is called *garbage collection*. Garbage collection usually takes place in two phases. First, the process runs through all the lists, tagging those cells, which are currently in use. In the second phase, the process runs through memory, collecting all untagged blocks and inserting the same in free pool. In general, garbage collection takes place when either overflow or underflow occurs. In addition, when the CPU is idle, the garbage collection starts. Note that the garbage collection is invisible to the programmer.

*Overflow* Sometimes, a new data node is to be inserted into data structure, but there is no available space, that is, free pool is empty. This situation is called *overflow*.

**Underflow** This refers to the situation where the programmer wants to delete a node from the empty list. The most suitable data structure for garbage collection is circular DLL. It allows the process of search to be unending traversal through list process as it is circular; DLL allows to traverse on both sides.

## RECAPITULATION

- Linear list is the list where each element has a unique predecessor and a unique successor. Linear lists are of two categories, namely general and restricted. General list is the one where data can be inserted or deleted anywhere in the list, whereas in restricted lists, there are a few restrictions. Linear list can be implemented using arrays and pointers. An implementation that uses pointers and dynamic memory allocation is called as linked list. A linked list is a very effective and efficient dynamic data structure. Items may be added or deleted from it at any position much easily as compared to arrays. Linked lists are useful data structures, especially if you need to automatically allocate and de-allocate space in a list. The basic operations are create list, traverse the list, insert, and delete a node. There are two variations of linked list, namely SLL and DLL. Both the linked lists can be circular lists. The linked list could be with or without a header node. Header node is used to store some information about the list so that it can be accessed without traversing the same. Information could be total number of nodes in the list, and similarly any other. Linked list is the most popular data structure used. It has many applications such as process queue, print queue, garbage collection, and so on.

## KEY TERMS

- **Circular linked list** The linked list whose link field of last node is set to point to the first node rather than `null` is called a circular linked list.
- **delete operator** To destroy a dynamically allocated variable/object and free the space for the object, the operator `delete` is used.
- **Doubly linked list** In doubly linked list, each node has two link fields to store information about the one next to and also about the one ahead of the node. Hence, each node has knowledge of its successor and also its predecessor. In doubly linked list, the list can be traversed in both the directions from every node.
- **Dynamic memory allocation** The process of allocating memory at run-time is known as dynamic memory allocation.
- **Generalized lists** Generalized lists are defined recursively as lists whose members may be single data elements or other generalized lists. A generalized list is a linear list (non-indexed) of zero or more data elements or generalized lists. In other words, a generalized list is a finite sequence of n >= 0 elements, alpha_1, alpha_2 ... alpha_n, which we write as list A = (alpha_1, alpha_2, ... alpha_n), where alpha_i is either an atom or a list. The elements of alpha_i where 1 <= i <= n, which are not atoms are said to be the sub-lists of list.
