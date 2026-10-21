
Thus, a solution similar to the non-inline functions for the templates is needed. It is possible using another model that uses the keyword export (discussed in the following section), where it is possible to define a template function at a single place and use declarations at other places.

## export Keyword

The keyword export is useful when a template function is defined at a single place and the declarations are used at other places. This is useful in instances where the templates defined while developing one application are found to be useful for other applications or when the templates designed by somebody else are to be used.

Suppose we define BubbleSort.cpp to contain the definition of the generic bubble sort. Then, it is possible to modify the definition as follows:

```
export template <typename Type>
void GenericBubbleSort(Type TempIntArray[])
{
    Body of the function
}
```

> Note In separate compilation model, the definition of the template definition is preceded by the keyword export in the file in which the templates are defined. In all other files, only the prototype of the template is specified.

If we want to use the same GenericBubbleSort() in UseIt.cpp, then the code in UseIt.cpp contains only the following:

```
{
    template <typename Type>
    void GenericBubbleSort(Type TempIntArray[]);
    /* Note the semicolon; it indicates the end */
    // No definition of the template
    // Other code
}
```

However, while linking UseIt.cpp, we just need to provide the .obj file of the BubbleSort program.

Note that in the earlier case the entire body of GenericBubbleSort() should be copied to UseIt.cpp.

The first model where template definitions are copied to all the files is called inclusion compilation model and the second one is known as separate compilation model as implementation is separated from the interface here.

## 7.5 USE OF typename

The keyword typename indicates that the expression following the keyword is the name of a type. We have used typename in the <> section in the template. It can also be used within the body of the template function (or template class function).

If we write a typename identifier, then that identifier is treated as a type in that function template as shown in Program 7.12.

### PROGRAM 7.12 Using typename for unambiguously specifying a type

```
//Typename.cpp
#include <iostream>
using namespace std;

int ptr;
template <class Type>

void Min()
{
    typename Type::Test * ptr;
    // Type::Test *ptr;
    // Other code, which does not concern us here
}

class TestTypeName1
{
public:
    typedef int Test;
};

class TestTypeName2
{
public:
    typedef char Test;
};

void main()
{
    Min <TestTypeName1>();
    Min <TestTypeName2>();
}
```

## How the Program Works

Here, we have two classes, TestTypeName1 and TestTypeName2, both of which define a type Test. Min() is a function template with a single Type argument. We have called this function twice, first with the argument TestTypeName1 and the second time with TestTypeName2. When Type is instantiated by TestTypeName1, Type::Test is an integer and when Type is instantiated by TestTypeName2, it is a char. The user here wants to define a variable of type Test. This means that if TestTypeName1 is the argument, then the variable is int, and if TestTypeName2 is the argument, then the variable is char. To define that we cannot write the statement,

```
Test Variable;
```

as it would confuse the compiler that there are two different options

We need to write the following statement as it would not create any ambiguity:

```
Type::Test Variable;
```

We have to refer to it as TestTypeName1::Test if we want to have the Test data type of the first class (which is actually an int). Likewise, we have to write TestTypeName2::Test, which is actually a char, when we are referring to the type of the second class TestTypeName2. The Type contains that type, so the ambiguity no longer exists.

Note that the scope resolution operator is used here to avoid confusion about the Test we are referring to, because we have two different data types having the same name. The name we have used with the class name and the scope resolution operator is known as the qualified name.

Now, suppose we need to define a pointer to this type Test. Our definition now changes to

Type::Test * ptr;

which is a source of ambiguity. Why?

A statement such as Type::Test * ptr; is valid and acceptable, but the problem is that the use of '*' is ambiguous. Why?

It can be interpreted in two different ways; the first one is what we intend here, that is, defining a pointer pointing to the type Type::Test; it can also be assumed to be a multiplication operation where the result is ignored (i.e., multiplying Test with ptr and ignoring the outcome). The compiler may take that meaning by default. If we want to treat Type::Test as type, we have to tell the compiler explicitly, which we have done in this program by writing typename before the definition.

typename Type::Test * ptr;

It is also possible that the compiler may take the intended meaning by default, but by writing typename before the definition, we make the program more portable. It makes a program independent of the defaults of a given compiler by compiling the program using any another compiler.

## RECAPITULATION

- Templates are very helpful in achieving software reusability.
- Templates are type-independent outlines of definitions of classes and functions.
- It is possible to later on instantiate real classes and functions with specific type using these templates.
- Function templates are outlines of generic functions and class templates are outlines of generic classes.
- When a specific class or function is instantiated with some specific type, the body of the instantiation will replace the generic type with the specific type.
- Argument deduction is possible for function templates.
- A function template can have multiple arguments similar to the normal function.
- We can have specializations that are different from what the compiler otherwise provides. This means that we can always override a specific specialization by providing our own explicit version.
- One template can be overloaded with another by providing different numbers of arguments, as different types cannot be specified.
- Though it is allowed to provide default arguments to a class template, it is not allowed for the function template.
- Static data members of the class templates are instantiated once for one instantiation of the class.
- It is possible to overload the class template with another class template having type specification as a subset of the original type specification. This overloading of class template is known as partial specialization.
- When we are dealing with multiple source files, it is possible to copy the template definitions to all the files, compile each file separately, and then create an executable file.
- It is also possible to define member functions and template functions of template classes at a single place, and use them in other files with just declarations. In this case, the definitions are to be preceded by the keyword export.
- typename is the keyword that allows the users to specify an expression as a data type, overriding any default meaning that the expression may stand for.

## KEYWORDS

**Class template** This is a generic class outlined by the specification of a generic type using the keyword template. The actual class is defined later using this template.

**Explicit specialization** When either a function or a class is defined explicitly for a specific type, then that special definition is known as explicit specialization.

(d) template <typename T>; void fun(T var1);

9. Is there any restriction on the number of arguments as well as the number of types passed to template functions? (a) Yes (b) No (c) Only when the template function is defined outside the class (d) Only when the template function defined inside the class

10. What are the classes Stack <int> and Stack <char> known as? (a) Normal classes (b) Template classes (c) Specializations (d) Special classes

# Conceptual Exercises

1. What is the need for template functions in C++? What are their advantages?
2. What are the problems with using macros? Explain using an example other than the one given in the book.
3. Give a few examples of multi-argument templates.
4. What is the difference between typename and class?
5. What is instantiation? Explain.
6. What is the need for operator overloading when we are using template functions to work with user-defined types? Clarify with an example.
7. What is the difference between generic and non-generic (type and non-type) arguments to function templates?
8. What is the difference between a template function and template class?
9. What are the advantages of template arguments deduction? When is it not possible for the compiler to deduce the argument types?
10. Give a few examples where explicit specialization of template function and template class is required.
11. Why do we need to overload a normal function instead of template specialization in some cases? Give an example to explain the need.
12. Give an example explaining the need for overloading a template with another template.
13. Discuss the efficiency and flexibility issues with templates.
14. What is the difference between manually overloaded functions and template instantiations?
15. Give an example where using the default arguments are useful in class template.
16. How does the behaviour of the static data members of a class template differ from that of static data members of a normal class?
17. What is the need for partial specialization? Differentiate between explicit specialization and partial specialization.
18. Explain the two models for template compilation? Compare.
19. Explain how typename can be used to indicate the type giving an example.

# Practical Exercises

1. Implement selection sort as a generic function.
2. Implement quick sort as a generic function.
3. Write a program for binary search as a generic function. The function should take arguments as array name, the size, and the element to be searched.
4. Implement selection sort with a non-type size.
5. Implement quick sort with a non-type size.
6. Write a program for generic queue class with two member functions, insert and delete. Use the array to implement the queue.
7. Use the queue class in the previous problem and provide specialization for strings.
