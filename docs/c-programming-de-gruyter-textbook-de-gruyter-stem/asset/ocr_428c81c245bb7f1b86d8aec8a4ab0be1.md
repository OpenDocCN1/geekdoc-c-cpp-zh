# 216 6 Arrays, Pointers, Strings

i pointed by i_pointer. Here, both the value of i and *i_pointer are 10. The former is direct access, and the latter is an indirect access by the pointer.
*i_pointer appears twice in the program, though its meanings are different. In the pointer declaration statement, **before the identifier that declared the identifier is a pointer; in the output statement, ** is the pointer operator that leads an indirect access to the variable that the pointer points to.
Several points should be noted about the type of pointer.

+   1. We can declare a pointer to a constant. In this case, we cannot change the value of the object through the pointer, although the value of the pointer itself can be changed to point to other objects. For example,

```
const char *name1= "John";n//name1 is a pointer which points to a const
char s[]="abc";nname1=s;
//correct, the value of name1 can be changed
*name1='1';
//compiling error, the value of the object that name1 points to
//cannot be changed through name1
```

Using a pointer that points to a constant can avoid the object from being changed accidentally. If we use a general pointer to store the starting address of a constant, the compiler cannot ensure that the object pointed by remains unchanged, and errors may occur during the running time. The following program segment is an example.

```
char *name1 = "John";n//name1 is a general pointer, but it stores the starting address
//of a string constant
*name1='A';
//compilation succeeds, but error in running. The content of the
//string constant cannot be changed.
```

Here, we try to change characters of the string constant "John" through pointer name1. Because name1 is a general pointer, the compiler is unaware of its error. But it goes wrong when running the program. In this situation, we should declare name1 as a pointer that points to a string constant.

+   2. We can declare a constant of the pointer type, and the value of the pointer cannot be changed during the execution of the program. For example,

```
char *const name2 = "John";nname2="abc";n//error, name2 is a pointer constant, and its value cannot be changed
//changed
```

+   3. In general, the value of a pointer can only be assigned to pointers of the same type. But there is a special kind of pointers that belong to the void type. Such a pointer