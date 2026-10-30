exactly what happens!

# B.2.2 General strategy

The preceding discussion might suggest the following strategy for managing memory using shared_ptr:

+   1. First write the program without worrying about memory management, i.e. use ordinary pointers and allocate memory but do not worry about returning it.

+   2. Replace every pointer which can potentially point to heap allocated memory with a shared_ptr.

+   3. Initialize/assign to shared_ptr only by a new object, or by the value of another shared_ptr or by NULL. Note that as in the preceding program, you cannot write shared_ptr<A> s1 = new A;, but you must explicitly convert the pointer to a shared_ptr.

This strategy works well sometimes. For example, it works quite well for the derivative finding program. We discuss this in Section B.2.3.

This strategy may not work, for several reasons. One possibility is that you may have pointers for which rule 3 above cannot be applied, because originally they were being used to hold new addresses as well as addresses of variables in activation frames. In this case you will need to reorganize your program.

However, any implementation of reference counting (including that provided by shared_ptr) has one fundamental limitation: if your pointers form cycles, then you will have memory leaks even with shared_ptrs. We will see this in Section B.2.4.

# B.2.3 Shared pointer in derivative finding

We first develop the code which does not worry about returning dynamic memory. For this we use the representation for trees developed in Section 22.1.3. The code is shown in Figure B.3.

First we have a constructor for constructing terminal or literal nodes. Then we have the constructor for non-leaf nodes. These follow along the lines of Section 22.1.3. Next we have functions Sum, Prod and Lit that include the new operator and thus create the node on the heap. These are convenient to use and the main program at the end uses them. Then we have a str function which converts the expression represented by the subtree underneath the node into a string.

Finally, we have the deriv function. This uses the definition: the derivative of a sum is the sum of the derivatives, the derivative of a product is as per the rule discussed above, and the derivative of a literal is 1 if and only if the literal is x.

To this code we can apply our recipe for adding in shared_ptrs. We only have one kind of pointer in this code: Exp*. And as you can see, it is always used to point to heap allocated objects. Also, the pointer structures created in this program will not have cycles. So we do the following:

+   1. Replace every Exp* with shared_ptr<Exp>. For this it is better to define typedef shared_ptr<Exp> spE;, and then replace Exp* by spE.