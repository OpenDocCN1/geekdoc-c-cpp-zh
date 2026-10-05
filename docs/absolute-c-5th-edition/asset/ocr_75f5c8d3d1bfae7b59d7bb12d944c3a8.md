# Syntax for Class Templates

The syntax details for class templates are basically the same as those for function templates. The following is placed before the template definition:

```
template<class T>
```

The parameter T is used in the class definition just like any other type. With function templates, the parameter T represents a type that can be any type at all; the parameter does not have to be replaced with a class type. With function templates, you may use any (non)class identifier instead of T, although it is traditional to use T.

Display 16.4 shows an example of a class template. An object of this class contains a pair of values T: If T is int, the values are pairs of integers; if T is char, the object values are pairs of characters, and so on.

Once the class template is defined, you can declare objects of this class. The declaration must specify what type to be filled in for T. For example, the following declares the object score so it can record a pair of integers, and it declares the object pair

```
Pair<int> score;
Pair<char> seats;
```

The objects are then just like any other objects. For example, the following score to be 3 for the first team and 0 for the second team:

```
score.setFirst(3);
score.setSecond(0);
```

Display 16.4 Class Template Definition (part 1 of 2)

```
// Class for a pair of values of type T:
template<class T>
class Pair
{
public:
    Pair( );
    Pair(T firstValue, T secondValue);
    void setFirst(T newValue);
    void setSecond(T newValue);
    T getFirst() const;
    T getSecond() const;
private:
    T first;
    T second;
};
```

> ^Pair is a template version of the class intPair given in Display 8.6. However, since you would not be appropriate for all types T, we have omitted the increment and decrement operators.