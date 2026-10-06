# 6.2 Pointers — 229

```
p1=&;
//assign the pointer the address of
//object A
cout<<p1->GetX()<<endl;
//Using pointer to access the
//object's member
cout<<A.GetX()<<endl;
//Using object name to access the
//object's member
```

An object pointer must be assigned to a declared object before being used. We can access the public members of an object using an object pointer.

In Chapter 4, we used the following program segment as an example to introduce forward reference declaration:

```
class Fred; //forward reference declaration
class Barney {
Fred x; //error: the definition of class Fred is not complete
};
class Fred {
Barney y;
};
```

We already know that this program segment is wrong. But if it can be slightly modified as follows, the grammar will be correct.

```
class Fred; //forward reference declaration
class Barney {
Fred *x;
};
class Fred {
Barney y;
};
```

Here, one is allowed to declare a pointer (not object) of class Fred in class Barney. Since the definition of Fred is after the definition of Barney, we can naturally declare an object of class Barney as a data member of class Fred. Therefore, this program is correct.

# 2. this pointer

The pointer is a special pointer hidden in every member function (including the constructor and destructor) of a class, and is used to point to the object currently processed by the member function.

Let's first review the situation where we use the Point class to solve the linear regression problem in the last section: in an array, there are many objects in the Point class, and we use array subscripts to identify them. In the initialization of each object, we need to call the constructor. The statements in a constructor body are: