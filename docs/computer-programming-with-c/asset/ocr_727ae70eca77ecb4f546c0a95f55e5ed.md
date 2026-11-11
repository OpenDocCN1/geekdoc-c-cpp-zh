ERROR on compilation of this program is as follows:

![](bbox=[0.208, 0.139, 0.804, 0.205])

> **NOTES**
> 
> To create a pointer that can point to a constant value, you can also put keyword `const` in between data type and asterisk symbol.
> 
> The statement
> 
> ```cpp
> const int* p=&a;
> ```
> 
> is equivalent to
> 
> ```cpp
> int const *p=&a;
> ```
> 
> Both the statements create a pointer `p` that points to constant. You can use any one of the syntax in your program.

# 8.5.4  Constant pointer that points to a constant value

We can also create a constant pointer that points to a constant value. This means that we will neither be able to change address contained inside the pointer nor the value that the pointer points to. Such pointers can be initialized only once during their creation. In order to create such pointers, the keyword `const` must appear at two places in the pointer declaration as shown in the following syntax:

```
const DataType* const pointer_name=&Target_Variable;
```

The statement,

```
const int* const p=&a;
```

will create a pointer p as a constant pointer that points to a constant value. Hence, both the statements,

```
p=&b;  /*Error - cannot change the address contained in pointer*/
*p=(*p)+1; /*Error - cannot change the value pointed by pointer*/
```

will give an error because you can neither change the address contained inside the pointer nor the value that the pointer points to.

> **NOTES**
> 
> An array is internally created using a constant pointer which points to the first element of the array. This pointer has a same name as that of the name given to the array. Indeed, the array name is actually the name of the constant pointer, using which array elements are accessed.