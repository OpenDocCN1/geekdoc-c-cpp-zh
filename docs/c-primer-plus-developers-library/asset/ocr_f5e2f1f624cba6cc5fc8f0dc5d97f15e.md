```
```cpp
        items[top++] = item;
        return true;
    }
    else
        return false;
}

template <class Type>
bool Stack<Type>::pop(Type & item)
{
    if (top > 0)
    {
        item = items[--top];
        return true;
    }
    else
        return false;
}

#endif
```
```

# ## Using a Template Class

Merely including a template in a program doesn't generate a template class. You have to ask for an instantiation. To do this, you declare an object of the template class type, replacing the generic type name with the particular type you want. For example, here's how you would create two stacks, one for stacking ints and one for stacking string objects:

```
```cpp
Stack<int> kernels;      // create a stack of ints
Stack<string> colonels;  // create a stack of string objects
```
```

Seeing these two declarations, the compiler will follow the Stack<Type> template to generate two separate class declarations and two separate sets of class methods. The Stack<int> class declaration will replace Type throughout with int, and the Stack<string> class declaration will replace Type throughout with string. Of course, the algorithms you use have to be consistent with the types. The stack class, for example, assumes that you can assign one item to another. This assumption is true for basic types, structures, and classes (unless you make the assignment operator private) but not for arrays.

Generic type identifiers such as Type in the example are called type parameters, meaning that they act something like variables, but instead of assigning a numeric value to a type parameter, you assign a type to it. So in the kernel declaration, the type parameter Type has the value int.

Notice that you have to provide the desired type explicitly. This is different from ordinary function templates, for which the compiler can use the argument types to a function to figure out what kind of function to generate: