# 11.6.2 Compatibility and Efficiency Issues

The following are a few other RTTI-related issues:

Backward compatibility with C-style casting It is important to note that compatibility with C is a major concern to C++ designers. C-style casting is still being used in a number of programs. It is not recommended to use it in newer C++ programs though.

Efficiency Using RTTI is not efficient. Even if one does not use typeid or dynamic_cast, the program runs slowly when RTTI is enabled. It is because the information about type using typeinfo object is added to every polymorphic type. The typeinfo objects are to be constructed and destroyed similar to other objects, which ultimately slows down the execution.

Using virtual functions in place of RTTI If possible, one must use virtual functions in place of RTTI because they are more efficient. However, it is not possible to use virtual functions in place of RTTI in some cases.

Note C-type cast is still heavily used; however, a good design should use better casting operators mentioned in this chapter.

# 11.7 CROSS CASTING

Cross casting refers to casting from the derived to the proper base class when there are multiple base classes in case of multiple inheritance.

Consider Program 11.12, which has the following statements:

```
class Derived : public Base1, public Base2;
Base1 *Base1Ptr = new Derived;
Base2 *Base2Ptr;
```

Let us see what happens when one writes

```
Base2Ptr = Base1Ptr;
```

First of all, one needs to make sure that it is allowed. Fortunately, in this case, the compiler allows and automatically adjusts the pointer to point to the base class subobject of the derived class. The value of Base1Ptr pointer is incremented to make it point to Base2 subobject of the derived class and then assigned to the Base2Ptr pointer. Thus, in this case, the behaviour of the assignment statement seems valid.

There are two classes, Base1 and Base2, and Derived is derived from both Base1 and Base2 (multiple inheritance). Now, casting the Base1 pointer, pointing to a derived class object, to Base2 is valid when the object is of type Derived. (Since Base1 and Base2 are both base classes of Derived, their pointers can point to the derived class object.) The problem is that the Base2Ptr pointer should only be able to address the Base2 subobject of the derived class. This is why the compiler intervenes and does what has been discussed here.

Unfortunately, when a pointer is casted using C-style casting, this does not happen. Have a look at the following statement:

```
Base2Ptr = (Base2 *) Base1Ptr;
```

Thus, if casting is used instead, what one gets is not what one wants. The address value in the pointer is not incremented to make it point to the Base2 subobject of the derived class.