# CHAPTER 17 Linked Data Structures

# The Arrow Operator, ->

The arrow operator, ->, specifies a member of a struct or a member of a class object that is pointed to by a pointer variable. The syntax is
```c
Pointer_Variable->Member_Name
```

\nThis refers to a value of a member of the struct or class object pointed to by the Pointer_Variable. Which member it refers to is given by the Member_Name. For example, suppose you have the following definition:

```
struct Record
{
    int number;
    char grade;
};
```

The following creates a dynamic variable of type Record and sets the member variables of the dynamic struct variable to 2001 and 'A':

```
Record *p;
p = new Record;
p->number = 2001;
p->grade = 'A';
```

Look at the pointer member in the last node in the list shown in Display 17.2. This last node has the word NULL written where there should be a pointer. In Display 17.1, we filled this position with the phrase "end marker," but "end marker" is not a C++ expression. In C++ programs we use the constant NULL as a signal to indicate the end of a linked list (or the end of any other kind of data structure).

NULL is typically used for two different (often coinciding) purposes. First, NULL is used to give a value to a pointer variable that otherwise not have any value. This prevents an inadvertent reference to memory, since NULL is not the address of any memory location. The second category of use is that of an end marker. A program can step through the list of nodes as shown in Display 17.2 and know that it has to come to the end of the list when the program reaches that node contains NULL.

As noted in Chapter 10, the constant NULL is actually the number 0, but we prefer to think of it and spell it as NULL to make clear that it means this special-purpose value you can assign to pointer variables. The definition of the identifier NULL is in number of the standard libraries, such as <iostream> and <cstddef>, so you should use an include directive with either <iostream>, <cstddef>, or some other suitable library when use NULL. The definition of NULL is handled by the C++ preprocessor, which replaces NULL with 0. Thus, the compiler never sees "NULL", so are no namespace issues; therefore, no using directive is needed for NULL.