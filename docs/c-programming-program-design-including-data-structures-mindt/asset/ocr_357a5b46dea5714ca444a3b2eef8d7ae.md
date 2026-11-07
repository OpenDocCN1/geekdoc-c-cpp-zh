From the output of the statements in Lines 20 and 21, it follows that `radiusPtr` stores the address of the variable `radius`. (Note that the address of `radiusPtr`, the value of `radiusPtr`, and the address of `radius` as shown by the output of Lines 19, 20, and 21, respectively, are machine dependent. When you run this program on your machine, you are likely to get different values. Furthermore, the pointer values, that is, the addresses, are printed in hexadecimal by default.)

# # Classes, Structs, and Pointer Variables

In the previous section, you learned how to declare and manipulate pointers of simple data types, such as `int` and `char`. You can also declare pointers to other data types, such as classes. You will now learn how to declare and manipulate pointers to classes and structs. (Recall that both classes and structs have the same capabilities. The only difference between classes and structs is that, by default, all members of a class are `private`, and, by default, all members of a `struct` are `public`. Therefore, the following discussion applies to both.)

Consider the following declaration of a `struct`：

```
```cpp
struct studentType
{
    char name[26];
    double gpa;
    int sID;
    char grade;
};

studentType student;
studentType* studentPtr;
```
```

In the preceding declaration, `student` is an object of type `studentType`, and `studentPtr` is a pointer variable of type `studentType`. The following statement stores the address of `student` in `studentPtr`：

```
```cpp
studentPtr = &student;
```
```

The following statement stores 3.9 in the component `gpa` of the object `student`：

```
```cpp
(*studentPtr).gpa = 3.9;
```
```

The expression `(*studentPtr).gpa` is a mixture of pointer dereferencing and the class component selection. In C++, the dot operator, `.`, has a higher precedence than the dereferencing operator.

Let us elaborate on this a bit. In the expression `(*studentPtr).gpa`, the operator `*` evaluates first, so the expression `*studentPtr` evaluates first. Because `studentPtr` is a pointer variable of type `studentType`, `*studentPtr` refers to a memory space of type `studentType`, which is a `struct`. Therefore, `(*studentPtr).gpa` refers to the component `gpa` of that `struct`.