This definition of the class template `listType` is a generic definition and includes only the basic operations on a list. To derive a specific list from this list and to add or rewrite the operations, we declare the array containing the list elements and the length of the list as `protected`.

Next, we describe a specific list. Suppose that you want to create a list to process integer data. The statement

```
```cpp
listType<int> intList;                    //line 1
```
```

declares `intList` to be an object of `listType`. The `protected` member `list` is an array of 100 components, with each component being of type `int`. Similarly, the statement

```
```cpp
listType<newString> stringList;           //line 2
```
```

declares `stringList` to be an object of `listType`. The `protected` member `list` is an array of 100 components, with each component being of type `newString`.

In the statements in Lines 1 and 2, `listType<int>` and `listType<newString>` are referred to as *template instantiations* or *instantiations of the class template `listType<elemType>`*, in which `elemType` is the class parameter in the template header. A template instantiation can be created with either a built-in or user-defined type.

The function members of a class template are considered function templates. Thus, when giving the definitions of the function members of a class template, we must follow the definition of the function template. For example, the definition of the member `insert` of the class `listType` is:

```
```cpp
template <class elemType>
void listType<elemType>::insert(elemType newElement)
{
    .
    .
    .
}
```
```

In the heading of the member function’s definition, the name of the class is specified with the parameter `elemType`.

The statement in Line 1 declares `intList` to be a list of 100 components. When the compiler generates the code for `intList`, it replaces the word `elemType` with `int` in the definition of the class `listType`. The template parameter in the definitions of the member functions (for example, `elemType` in the definition of `insert`) of the class `listType` is also replaced by `int`.

# HEADER FILE AND IMPLEMENTATION FILE OF A CLASS TEMPLATE

Until now, we have placed the definition of the class (in the header file) and the definitions of the member functions (in the implementation file) in separate files. The object code was generated from the implementation file and linked with the user code. However, this mechanism of separating the class definition and the definitions