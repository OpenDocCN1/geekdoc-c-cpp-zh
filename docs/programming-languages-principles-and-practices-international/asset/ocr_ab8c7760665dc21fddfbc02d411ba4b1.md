data types, or at least for the IntArray specification. To make the final and initial semantics agree, however, we must add the axiom

```
insertIA (insertIA(A,i,j),k,m) = insertIA (insertIA(A,k,m),i,j)
```

In the case of the queue algebraic specification, the final and initial semantics already agree, so we don’t have to worry: given two queues p and q,

```
p = q if and only if p = createq and q = createq
or frontq(p) = frontq(q) and dequeue(p) = dequeue(q)
```

# Exercises

+   11.1 Discuss how the following languages meet or fail to meet criteria 1 and 2 for an abstract data type mechanism from the beginning of this chapter:
+   (a) C
+   (b) Ada
+   (c) ML
+   (d) another language of your choice.

11.2 In the algebraic specification of the complex abstract data type in Section 11.1, axioms were given that base complex addition and subtraction on the corresponding real operations. Write similar axioms for (a) multiplication and (b) division.

11.3 An alternative to writing axioms relating the operations of complex numbers to the corresponding operations of their real and imaginary parts is to write axioms for all the usual properties of complex numbers, such as associativity, commutativity, and distributivity. What problems do you foresee in this approach?

11.4 Finish writing the abstype Complex definition of Figure 11.2 in ML (Section 11.2).

11.5 Finish writing the implementation of package ComplexNumbers in Section 11.4.

11.6 Write a complex number module in C using the header file approach described in Section 11.3.

11.7 Use your implementation of Exercise 11.4, 11.5, or 11.6 to write a program to compute the roots of a quadratic equation ax2 + bx + c = 0. (a, b, and c may be assumed to be either real or complex.)

11.8 Write a new implementation for complex numbers in C, Ada, or ML that uses polar coordinates. Make sure that your interface and client code (e.g., Exercise 11.7) do not change.

11.9 Write an implementation for the queue ADT in C or Ada that uses a doubly linked list with front and rear pointers instead of the singly linked list with rear pointer that was used in this chapter. Make sure that your interface and client code do not change.

11.10 Rewrite the abstype Complex in ML as a signature and structure.

11.11 Implement the Stack ADT as described in Section 11.1 in (a) C; (b) Ada; (c) ML.

11.12 A double-ended queue, or deque, is a data type that combines the actions of a stack and a queue. Write an algebraic specification for a deque abstract data type assuming the following operations: create, empty, front, rear, addfront, addrear, deletefront, and deleterear.

11.13 Which operations of the complex abstract data type of Section 11.1 are constructors? Which are inspectors? Which are selectors? Which are predicates? Based on the suggestions in Section 11.1, how many axioms should you have?