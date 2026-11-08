a way to avoid this pitfall. To avoid this shallow copying of data for classes with a pointer member variable, C++ allows the programmer to extend the definition of the assignment operator. This process is called overloading the assignment operator. Chapter 13 explains how to accomplish this task by using operator overloading. Once the assignment operator is properly overloaded, both `objectOne` and `objectTwo` have their own data, as shown in Figure 12-17.

![](bbox=[0.211, 0.239, 0.953, 0.368])

# Copy Constructor

When declaring a class object, you can initialize it by using the value of an existing object of the same type. For example, consider the following statement:

```
ptrMemberVarType objectThree(objectOne);
```

The object objectThree is being declared and is also being initialized by using the value of objectOne. That is, the values of the member variables of objectOne are copied into the corresponding member variables of objectThree. This initialization is called the default member-wise initialization. The default member-wise initialization is due to the copy constructor, called the copy constructor (provided by the compiler). Just as in the case of the assignment operator, because the class ptrMemberVarType has pointer member variables, this default initialization would lead to a shallow copying of the data, as shown in Figure 12-18. (Assume that objectOne is given as before.)

![](bbox=[0.312, 0.771, 0.858, 0.902])