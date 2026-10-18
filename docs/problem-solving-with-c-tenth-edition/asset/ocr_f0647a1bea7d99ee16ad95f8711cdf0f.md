# 17.2 TEMPLATES FOR DATA ABSTRACTION

> Equal wealth and equal opportunities of culture . . . have simply made us all members of one class.

EDWARD BELLAMY, *Looking Backward: 2000–1887*

As you saw in the previous section, function definitions can be made more general by using templates. In this section, you will see that templates can also make class definitions more general.

# Syntax for Class Templates

The syntax for class templates is basically the same as that for function templates. The following is placed before the template definition:

```
template<class T>
```

The type parameter T is used in the class definition just like any other type. As with function templates, the type parameter T represents a type that can be any type at all; the type parameter does not have to be replaced with a class type. As with function templates, you may use any (nonkeyword) identifier instead of T.

For example, the following is a class template. An object of this class contains a pair of values of type T; if T is int, the object values are pairs of integers, if T is char, the object values are pairs of characters, and so on.

```
```cpp
//Class for a pair of values of type T:
template<class T>
class Pair
{
public:
    Pair();

    Pair(T firstValue, T secondValue);

    void setElement(int position, T value);
    //Precondition: position is 1 or 2.
    //Postcondition:
    //The position indicated has been set to value.

    T getElement(int position) const;
    //Precondition: position is 1 or 2.
    //Returns the value in the position indicated.
private:
    T first;
    T second;
};
```
```

Once the class template is defined, you can declare objects of this class. The declaration must specify what type is to be filled in for T. For example, the