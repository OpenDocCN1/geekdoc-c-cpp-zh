To avoid this situation, every recursive function must have at least one **terminating condition**. Hence, we have defined a recursive function as a function which calls itself **conditionally** and not unconditionally.

> > **NOTES**
> >
> > Every recursive function must have at least one terminating condition which terminates the recursion. This avoids crashing of program due to infinite number of activation frames being created on stack.

In this section, we will discuss different examples of recursive solutions which will work in both C and C++.

# What is a stack?

![](bbox=[0.141, 0.434, 0.183, 0.46])

Stack is a Last In First Out(LIFO) type of memory. It is called so because the value that you insert last in stack is first to come out. We can imagine stack as a bucket with one open end as shown below;

![](bbox=[0.455, 0.492, 0.525, 0.573])

As the memory area has only one end open, we can insert and remove values only from one of its ends. The process of inserting elements into the stack is called as pushing whereas the process of removing elements from stack is called as popping. To understand this concept lets us assume we have a simple stack which can store integer values. Let the stack be initially empty. If we push first value 10 in the stack, then the stack is as shown in below

![](bbox=[0.455, 0.68, 0.524, 0.759])

Now, when we push another value say 20, it will be placed on the top of the existing value because there is only one open end to push/pop values to/from stack. Hence, the new state of stack is as shown below:

![](bbox=[0.455, 0.825, 0.524, 0.903])