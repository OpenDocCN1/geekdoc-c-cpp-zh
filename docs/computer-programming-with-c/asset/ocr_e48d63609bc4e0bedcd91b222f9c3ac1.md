Pointer arithmetic’s will be heavily in the Section 8.6, which explains the process to access array elements by using pointers.

# ### 8.5.1  Keyword `const` with pointers

From Chapter 2, we understand that const is a keyword used to create constant variables. For example,

```
const int a=10;
```

creates a variable a with a constant value 10. As we have used a keyword const in the declaration of a, the value of variable a cannot change throughout the program. Any attempt to change the value of the variable a will raise a compile time error.

Keyword const can also be used with pointer declarations. const can be used to create following three types of pointers:

+   1. Constant pointer
+   2. Pointer that points to a Constant Data Value
+   3. Constant pointer that points to a constant variable (combination of both 1 and 2)

# ### 8.5.2  Constant pointer

A pointer which cannot change the address to which it points to is called a **constant pointer**. The following is the syntax for creating constant pointers.

```
DataType* const pointer_name=&Target_Variable;
```

Note the presence of keyword const which creates a constant pointer. The pointer named as pointer_name is initialized to hold the address of Target_Variable.

It is important to note that, when you declare a constant pointer it must always be initialized. The following declaration of a constant pointer is illegal,

```
int* const p;
```

because the pointer p is never initialized. The highlighted statement,

```
int a=10;
int* const p=&a;
```

is legal because it initializes the address of variable a in the constant pointer p. Hence, assuming address of variable a as 1000, pointer p points to variable a as shown in the Figure 8.19.

![](bbox=[0.481, 0.731, 0.843, 0.839])

As p is a constant pointer, you cannot change the address stored inside p by any means. This means that you cannot reinitialize p to point to any other variable. For example, if b is another integer type variable, the following statement will give an error,