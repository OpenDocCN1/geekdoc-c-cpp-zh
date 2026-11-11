![](bbox=[0.26, 0.149, 0.684, 0.327])

of O3). However, since O3 is a local variable of `main()`, we create a temporary object `res` inside the operator function to store the result of pre-increment operation. The value of member `a` inside object `res` is set to 11 by the following statement:

```
res.a=++a;
```

The object `res` is returned by the operator function and its values get initialized to O3 as shown in the Figure 13.15.

The next statement

```
O4 = O2++;
```

applies a postfix increment operation on object O2 and stores the result in object O4.

The operator `++` is used with object O2, and hence, the compiler will invoke the operator function using object O2. As the operator `++` is used in a postfix form, the compiler will invoke the operator function that takes one dummy argument of type `int`. Figure 13.16 explains the execution of the operator function. The object returned by the operator function gets initialized to object O4 as shown in the Figure 13.16.

![](bbox=[0.189, 0.718, 0.686, 0.894])