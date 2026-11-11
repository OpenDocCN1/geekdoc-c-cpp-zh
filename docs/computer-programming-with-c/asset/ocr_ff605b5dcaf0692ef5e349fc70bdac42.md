Note that, at this stage, the pointer is not pointing to any member. We have just declared a pointer that has the ability to point to a particular member or a member function.

# **Step 2: Bind the pointer to a specific member of a class**

After the pointer is declared, you must bind the pointer to a specific member. If delta is a member variable within class A and has a data type as B, you can bind the pointer ptr we created in step 1 to the member delta using the following syntax:

```
```
ptr = &A::delta;
```
```

&A::delta in the above statement should be read as address of member delta declared in class A. At this stage, the pointer named as ptr is attached to member delta of class A, which means that you can use pointer named ptr with any of the objects of the class to access the member delta of a particular object. For example, if you use the pointer ptr with object o1, system will access member delta of o1. Similarly, if ptr is used with another object o2, system will access the member delta of object o2. The syntax to use a pointer with a particular object is given in step 3.

Similar to pointer to member variables, you must also bind pointer to member functions before they can be used with any specific object to invoke the member function of that object. Let us assume that f1() is the member function of class A taking 2 arguments of data types d1 and d2, and having a return type as R. In this case, we can create the pointer pftr and bind it to member function f1() using the following syntax:

```
```
/*create the pointer named pftr to point to a member function of
    class A*/
R (A::*pftr)(d1,d2);
/*Bind the pointer with member function f1*/
pftr = &A::f1;
```
```

Note that, at this stage, we have not accessed any member or a member function using a pointer but we have just attached the pointer to a member/member function. To access any non-static member or a member function of a class, you will always need an object of the class.

# **Step 3: Access the member using object of class and a bindable pointer**

After the pointer is attached to a specific member, you can use it with any object. For example, let us assume that o1 and o2 are two objects of class A, then the statement

```
```
o1.*ptr = 10;
```
```

will set the value of member delta of object o1 to 10. This is because ptr is attached to delta. Similarly, the statement

```
```
o2.*ptr=55;
```
```

will set the value of member delta of object o2 to 55.