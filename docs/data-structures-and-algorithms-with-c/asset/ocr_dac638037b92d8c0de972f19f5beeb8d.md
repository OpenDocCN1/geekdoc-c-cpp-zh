```
[End of Loop]
6. Print: P->INFO
7. Set R = P
[End of Loop]
8. Return
```

# Convert Array to Singly Linked List

We can convert a singly linked list using an existing array. The following algorithm creates a node, stores an array element and appends it at the beginning of the existing list.

This algorithm creates a node and inserts it at the beginning of the list. _HEAD' is a pointer which holds the address of the HEADER of the linked list and ITEM is the value of the new node. NEW is a pointer which holds the address of the new node.

# Algorithm to Convert Linked-List from an existing Array

```
Algorithm: CONVERT (A, N, HEAD)
1. Set HEAD = NULL
2. Repeat steps 3 to 8 while N # -1
3. Allocated memory for New node
4. If NEW = NULL then Print: “Memory not Available” and Return
5. Set NEW->DATA = A[N-1]
6. Set NEW->LINK = HEAD
7. Set HEAD = NEW
8. Set N = N - 1
[End of loop]
9. Return
```

# Representation of polynomials using linked list

In this representation, the polynomial can also be represented by linking list and a node in the linked list represents a term in the polynomial.

At first, we have to store exponent/degree and coefficient of the polynomial f (x). For that, we have to define a structure as follows:

```
typedef struct poly
{
    int exp;
    int coef;
    struct poly *LINK;
} term;
poly *head;
```

We will always store terms of the polynomial in descending order of degree.

4x^6 + 2x^4 + 3x + 1 would be represented by linked list like:

![](bbox=[0.09, 0.83, 0.88, 0.9])

Figure 5.13:Linked list representation of polynomials