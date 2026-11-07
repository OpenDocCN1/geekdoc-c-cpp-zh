
Let us next execute the following statement:

```
delete [] second;
```

After this statement executes, the array pointed to by `second` is deleted. This action results in Figure 14-11.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_857_0.png)

**FIGURE 14-11** `first` and `second` after the statement `delete [] second;` executes

Because `first` and `second` point to the same array, after the statement:

```
delete [] second;
```

executes, `first` becomes invalid, that is, `first` (as well as `second`) are now dangling pointers. Therefore, if the program later tries to access the memory pointed to by `first`, either the program will access the wrong memory or it will terminate in an error. This case is an example of a shallow copy. More formally, in a **shallow copy**, two or more pointers of the same type point to the same memory; that is, they point to the same data.

On the other hand, suppose that instead of the earlier statement, `second = first;` (in Line A), we have the following statements:

```
second = new int[10];

for (int j = 0; j < 10; j++)
    second[j] = first[j];
```

The first statement creates an array of 10 components of type `int`, and the base address of the array is stored in `second`. The second statement copies the array pointed to by `first` into the array pointed to by `second` (see Figure 14-12).

![](img/1fbe55537254baeb2b5b7dbaf64956ae_857_1.png)

**FIGURE 14-12** `first` and `second` both pointing to their own data

Both `first` and `second` now point to their own data. If `second` deletes its memory, there is no effect on `first`. This case is an example of a deep copy. More formally, in a **deep copy**, two or more pointers have their own data.

From the preceding discussion, it follows that you must know when to use a shallow copy and when to use a deep copy.

## Classes and Pointers: Some Peculiarities

In the previous section, we discussed how to use the arrow notation to access class members via the pointer if a pointer variable is of a class type. Because a class can have pointer member variables, this section discusses some peculiarities of such classes. To facilitate the discussion, we will use the following class:

```
class ptrMemberVarType
{
public:
    ⋮
    ⋮
    ⋮
private:
    int x;
    int lenP;
    int *p;
};
```

Also, consider the following statements (see Figure 14-13):

```
ptrMemberVarType objectOne;
ptrMemberVarType objectTwo;
```

![](img/1fbe55537254baeb2b5b7dbaf64956ae_858_0.png)

**FIGURE 14-13** Objects `objectOne` and `objectTwo`

### Destructor

The object `objectOne` has a pointer member variable `p`. Suppose that during program execution, the pointer `p` creates a dynamic array. When `objectOne` goes out of scope, all of the member variables of `objectOne` are destroyed. However, `p` created a dynamic array, and dynamic memory must be deallocated using the operator `delete`. Thus, if the pointer `p` does not use the `delete` operator to deallocate the dynamic array, the memory space of the dynamic array would stay marked as allocated, even though it cannot be accessed. How do we ensure that when `p` is destroyed, the dynamic memory created by `p` is also destroyed? Suppose that `objectOne` is as shown in Figure 14-14.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_859_0.png)

**FIGURE 14-14** Object objectOne and its data

Recall that if a class has a destructor, the destructor automatically executes whenever a class object goes out of scope (see Chapter 12). Therefore, we can put the necessary code in the destructor to ensure that when objectOne goes out of scope, the memory created by the pointer p is deallocated. For example, the definition of the destructor for the class ptrMemberVarType is:

```cpp
ptrMemberVarType::~ptrMemberVarType()
{
    delete [] p;
}
```

Of course, you must include the destructor as a member of the class in its definition. Let us extend the definition of the class ptrMemberVarType by including the destructor. Moreover, the remainder of this section assumes that the definition of the destructor is as given previously—that is, the destructor deallocates the memory space pointed to by p.

```cpp
class ptrMemberVarType
{
public:
    ~ptrMemberVarType();
    .
    .
    .

private:
    int x;
    int lenP;
    int *p;
};
```

> **NOTE**  For the destructor to work properly, the pointer p must have a valid value. If p is not properly initialized (that is, if the value of p is garbage) and the destructor executes, either the program terminates with an error message or the destructor deallocates an unrelated memory space. For this reason, you should exercise extra caution while working with pointers.

### Assignment Operator

This section describes the limitations of the built-in assignment operators for classes with pointer member variables. Suppose that objectOne and objectTwo are as shown in Figure 14-15.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_860_0.png)

**FIGURE 14-15** Objects objectOne and objectTwo

Recall that one of the built-in operations on classes is the assignment operator. For example, the statement:

```
objectTwo = objectOne;
```

copies the member variables of objectOne into objectTwo. That is, the value of objectOne.x is copied into objectTwo.x, and the value of objectOne.p is copied into objectTwo.p. Because p is a pointer, this member-wise copying of the data would lead to a shallow copying of the data. That is, both objectTwo.p and objectOne.p would point to the same memory space, as shown in Figure 14-16.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_860_1.png)

**FIGURE 14-16** Objects objectOne and objectTwo after the statement `objectTwo = objectOne;` executes

Now, if objectTwo.p deallocates the memory space to which it points, objectOne.p would become invalid. This situation could very well happen if the class ptrMemberVarType has a destructor that deallocates the memory space pointed to by p when an object of type ptrMemberVarType goes out of scope. It suggests that there must be a way to avoid this pitfall. To avoid this shallow copying of data for classes with a pointer member variable, C++ allows the programmer to extend the definition of the assignment operator. This process is called overloading the assignment operator. Chapter 15 explains how to accomplish this task by using operator overloading. Once the assignment operator is properly overloaded, both objectOne and objectTwo have their own data, as shown in Figure 14-17.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_861_0.png)

**FIGURE 14-17**  Objects objectOne and objectTwo

### Copy Constructor

When declaring a class object, you can initialize it by using the value of an existing object of the same type. For example, consider the following statement:

```
ptrMemberVarType objectThree(objectOne);
```

The object objectThree is being declared and is also being initialized by using the value of objectOne. That is, the values of the member variables of objectOne are copied into the corresponding member variables of objectThree. This initialization is called the default member-wise initialization. The default member-wise initialization is due to the constructor, called the copy constructor (provided by the compiler). Just as in the case of the assignment operator, because the class ptrMemberVarType has pointer member variables, this default initialization would lead to a shallow copying of the data, as shown in Figure 14-18. (Assume that objectOne is given as before.)

![](img/1fbe55537254baeb2b5b7dbaf64956ae_861_1.png)

**FIGURE 14-18**  Objects objectOne and objectThree

Before describing how to overcome this deficiency, let us describe one more situation that could also lead to a shallow copying of the data. The solution to both these problems is the same.

Recall that as parameters to a function, class objects can be passed either by reference or by value. Remember that the class ptrMemberVarType has the destructor, which deallocates the memory space pointed to by p. Suppose that objectOne is as shown in Figure 14-19.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_862_0.png)

**FIGURE 14-19** Object objectOne

Let us consider the following function prototype:

```cpp
void destroyList(ptrMemberVarType paramObject);
```

The function destroyList has a formal value parameter, paramObject. Now consider the following statement:

```cpp
destroyList(objectOne);
```

In this statement, objectOne is passed as a parameter to the function destroyList. Because paramObject is a value parameter, the copy constructor copies the member variables of objectOne into the corresponding member variables of paramObject. Just as in the previous case, paramObject.p and objectOne.p would point to the same memory space, as shown in Figure 14-20.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_862_1.png)

**FIGURE 14-20** Pointer member variables of objects objectOne and paramObject pointing to the same array
