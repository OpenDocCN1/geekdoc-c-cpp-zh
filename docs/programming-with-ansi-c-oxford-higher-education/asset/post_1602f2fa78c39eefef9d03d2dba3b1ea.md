
When we need to have a different behaviour for a different set of arguments, which is a subset of the original set of arguments, we need partial specialization.

```
...
public:
...
friend ClassNo1;
friend SomeNonTemplateFunction();
friend TemplateClassNo1;
friend TemplateClassNo2 <int>;
friend SomeTemplateFunction();
friend SomeTemplateFunction <int>()
// A specialization of template function
}
```

## 7.3.7 Primary and Partial Specialization

Suppose we want a specialization of the stack class that has been defined to work for pointer-to-any-variable in a different way (say, instead of storing pointers, we may need to store their contents). The specialization here should work for all types of pointers.

For example, if the employee objects are to be inserted in the stack, they are inserted without any change. In contrast, if the pointers to employee are inserted, then we insert their contents (i.e., employee objects pointed to by them). Similarly, if we need to push pointers to the passenger object in the stack, we again insert the contents pointed to by the pointer.

This process is distinctly different from normal overloading, which provides special treatment for only a single-type situation. However, here we are dealing with a set of types (all of type pointers in our case) for which we need a different behaviour. The specialization can be written as follows:

```
template <typename ElementType>
class Stack <ElementType*>
{ . . . }
```

Note the <ElementType *> appearing immediately after the class name. This indicates partial specialization. The code we have written would work for all pointer types. This is known as partial specialization.

> **Note** A partial specialization is a template definition that begins with a '< >' pair after the class name. It always follows the primary specialization. A primary specialization is the one that is defined before and of which the partial specialization is a subset.

A partial specialization should always follow the primary specialization, that is, a template definition without <> pair after the class name. In the given example, it relates to the following definition:

```
template <typename ElementType>
class Stack
{ . . . }
```

This is also applicable to the SafeArray. A special case is encountered when C-type strings are passed to the SafeArray. We need partial specialization because when we sort the array using techniques such as bubble sort, we need to compare strings and even assign one string to another.

Consider the following case as a definition of a generic safe array.

```
template <typename Type>
class SafeGenericArray
```

Suppose the following are the elements of the array:

```
template <typename Type>
class SafeGenericArray <Type *>
```

Though the content of first C-type string is the same as that of second C-type string, they are not similar because the addresses are not the same. We need to define another algorithm for manipulation in this case. Essentially, this is needed for any array containing pointers. Partial specialization can be used here. We have to define our specialization in the following template class:

```
template <typename Type>
class SafeGenericArray <Type *>
```

Now, it can work for any array as an element. Consider the following example that explains partial specialization.

The partial specialization solution is not ideal. See that the [] operator does not return a reference. This cannot be used in the LHS of the expression. Anyway, it serves the purpose of introducing partial specialization.

```
//PartSpec.cpp
#include <iostream>
using namespace std;
#define Size 10
#include <string.h>
template <typename Type>
class SafeGenericArray
{
    Type Array[Size];
public:
    Type & operator [](int Index)
    {
        if((Index < 0) || (Index > Size - 1))
        {
            cout << "Subscript out of range!";
            exit (1);
        }
        else
            return Array[Index];
    }
};
// The following is partial specialization
template <typename Type>
class SafeGenericArray <Type *>
{
    Type *Array[Size];
public:
    Type *operator[](int Index)
    {
        if((Index < 0) || (Index > Size - 1))
        {
            cout << "Subscript out of range!";
            exit(1);
        }
        else
        {
            cout << "Element no. " << Index << " is accessed \n";
            return Array[Index];
        }
    }
};
int main()
{
    SafeGenericArray <int> SafeIntArray1;
    SafeGenericArray <char> SafeCharArray1;
    
    SafeGenericArray <char *> SafeStringArray;
    char *String = "Lara";
    strcpy(SafeStringArray[1], String);
    SafeIntArray1[0] = 5;
    return 0;
}
```

## Output

Element no. 1 is accessed

We can also have multiple partial specializations for a single primary specialization, that is, we can have class SafeGenericArray <type &>, etc.

## 7.4 COMPILATION MODELS FOR TEMPLATES

When templates are included in the programs, there are two different ways to compile them. One is similar to inline functions where the template body is included when the templates are called; the other is similar to normal functions where the function call is replaced by some sort of jump instruction that calls the template function for a specified type and the control gets transferred to that place. Here we discuss both the types of compilation models.

### 7.4.1 Inline vs Non-inline Function Calls in Multiple Files

A very important difference between inline functions and normal functions is the way they are defined in a multifile program. It is possible to have a program that contains multiple files. Assume that Prog1.cpp, Prog2.cpp, and Prog3.cpp are three different files containing three different parts of the same program. To execute the program, the individual files are compiled one after another and then all the files are linked together to build a single executable file.

Suppose there is an inline function call in Prog1.cpp and Prog3.cpp. A copy of the function is needed in both the files. This is because inline functions are pasted at the time of compilation. If the individual file does not contain the body of the inline function, they cannot replace the call with the body.

> It is an error to define multiple copies of a non-inline function in multiple files.

This not the case with non-inline functions, which are defined only at a single place. Suppose, in the given example, a non-inline function xyz() is called from all the three .cpp files. If the function definition appears in Prog1.cpp; then only its declaration or prototype should appear in the other two files (as extern). The function body is not copied to the program at compile time. When all three files are linked together, they all have the call address of the same function.

It is actually an error if multiple copies of the same non-inline function are defined in multiple files. The compiler, at the time of compilation, cannot check this point; however, at the time of linking, when the linker gets multiple copies of the non-inline function, it would be unable to link the program.

> In multiple source files, inline functions need to have a source copy in all the files. In contrast, non-inline functions need to have only the extern definitions in all the files excluding the one where it is defined.

### 7.4.2 Template Instantiations in Multiple Files

In this section, we will learn if we need to define templates in every file where a template is to be instantiated, similar to inline functions. We will also learn whether it is possible to have the complete definition in one file and use it elsewhere with just the declaration. In other words, we will know whether template functions should be used like inline functions or non-inline functions.

In fact, both the models are applicable in the case of function templates. The templates can be defined in all the files that are being used. At the time of compilation, the compiler compiles the function as if it is the only definition. At the end of compilation, in a pre-link phase, when multiple copies of the same template instantiation are found, a single copy is taken and the others are ignored. There are a few problems with this approach, which are listed as follows:

- 1. It may not be possible to copy the template definitions in all the files as the template designer may not want the definition to be seen by others.
- 2. It may not be feasible to copy large template files to every file as it increases the compile time.
- 3. The template definition is an implementation and the template call is an interface. The interface should be separated from implementation for the following reasons:

(a) Implementation should be independently modifiable without changing the interface. Assume that template xyz is defined inside a file Prog1.cpp and is used in Prog2.cpp and Prog3.cpp. These two files should not be recompiled or recoded if the definition of xyz (implementation) changes.

(b) Implementation, at times, represents the high-quality work from a top-flight programmer. It is better that this is not distributed and is kept at a single place.

(c) Maintenance of the template becomes easy if the definition exists at a single place. If multiple copies of templates exist at multiple places, maintaining them can be problematic.

> One simple way to include templates in a multiple source file case is to copy all of them to all of the source files. It is called inclusion compilation model.

> When all template definitions are kept at a single place and linked with all other source files at linking time, it is known as separate compilation model.
