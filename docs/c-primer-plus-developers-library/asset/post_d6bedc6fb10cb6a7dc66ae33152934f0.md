
```cpp
void set(Student & sa, int n)
{
    cout << "Please enter the student's name: ";
    getline(cin, sa);
    cout << "Please enter " << n << " quiz scores:\n";
    for (int i = 0; i < n; i++)
        cin >> sa[i];
    while (cin.get() != '\n')
        continue;
}
```

Here is a sample run of the program in Listing 14.6:

```text
Please enter the student's name: Gil Bayts
Please enter 5 quiz scores:
92 94 96 93 95
Please enter the student's name: Pat Roone
Please enter 5 quiz scores:
83 89 72 78 95
Please enter the student's name: Fleur O’Day
Please enter 5 quiz scores:
92 89 96 74 64

Student List:
Gil Bayts
Pat Roone
Fleur O’Day

Results:
Scores for Gil Bayts:
92 94 96 93 95
average: 94

Scores for Pat Roone:
83 89 72 78 95
average: 83.4

Scores for Fleur O’Day:
92 89 96 74 64
average: 83
Done.
```

The same input as before leads to the same output that the containment version produces.

## Containment or Private Inheritance?

Given that you can model a *has-a* relationship either with containment or with private inheritance, which should you use? Most C++ programmers prefer containment. First, it's easier to follow. When you look at the class declaration, you see explicitly named objects representing the contained classes, and your code can refer to these objects by name. Using inheritance makes the relationship appear more abstract. Second, inheritance can raise problems, particularly if a class inherits from more than one base class. You may have to deal with issues such as separate base classes having methods with the same name or of separate base classes sharing a common ancestor. All in all, you're less likely to run into trouble using containment. Also containment allows you to include more than one subobject of the same class. If a class needs three string objects, you can declare three separate string members by using the containment approach. But inheritance limits you to a single object. (It is difficult to tell objects apart when they are all nameless.)

However, private inheritance does offer features beyond those provided by containment. Suppose, for example, that a class has protected members, which could either be data members or member functions. Such members are available to derived classes but not to the world at large. If you include such a class in another class by using composition, the new class is part of the world at large, not a derived class. Hence it can't access protected members. But using inheritance makes the new class a derived class, so it can access protected members.

Another situation that calls for using private inheritance is if you want to redefine virtual functions. Again, this is a privilege accorded to a derived class but not to a containing class. With private inheritance, the redefined functions would be usable just within the class, not publicly.

> **Tip**
>
> In general, you should use containment to model a *has-a* relationship. You should use private inheritance if the new class needs to access protected members in the original class or if it needs to redefine virtual functions.

## Protected Inheritance

Protected inheritance is a variation on private inheritance. It uses the keyword protected when listing a base class.

```cpp
    class Student : protected std::string,
                     protected std::valarray<double>
    {...};
```

With protected inheritance, public and protected members of a base class become protected members of the derived class. As with private inheritance, the interface for the base class is available to the derived class but not to the outside world. The main difference between private and protected inheritance occurs when you derive another class from the derived class. With private inheritance, this third-generation class doesn't get the internal use of the base-class interface. That's because the public base-class methods become private in the derived class, and private members and methods can’t be directly accessed by the next level of derivation. With protected inheritance, public base-class methods become protected in the second generation and so are available internally to the next level of derivation.

Table 14.1 summarizes public, private, and protected inheritance. The term *implicit upcasting* means that you can have a base-class pointer or reference refer to a derived class object without using an explicit type cast.

**Table 14.1 Varieties of Inheritance**

| Property | Public Inheritance | Protected Inheritance | Private Inheritance |
|---|---|---|---|
| Public members become | Public members of the derived class | Protected members of the derived class | Private members of the derived class |
| Protected members become | Protected members of the derived class | Protected members of the derived class | Private members of the derived class |
| Private members become | Accessible only through the base-class interface | Accessible only through the base-class interface | Accessible only through the base-class interface |
| Implicit upcasting | Yes | Yes (but only within the derived class) | No |

## Redefining Access with using

Public members of a base class become protected or private when you use protected or private derivation. Suppose you want to make a particular base-class method available publicly in the derived class. One option is to define a derived-class method that uses the base-class method. For example, suppose you want the Student class to be able to use the valarray sum() method. You can declare a sum() method in the class declaration and then define the method this way:

```cpp
double Student::sum() const      // public Student method
{
    return std::valarray<double>::sum(); // use privately-inherited method
}
```

Then a Student object can invoke Student::sum(), which, in turn, applies the valarray<double>::sum() method to the embedded valarray object. (If the ArrayDb typedef is in scope, you can use ArrayDb instead of std::valarray<double>.)

There is an alternative to wrapping one function call in another: use a using declaration (such as those used with namespaces) to announce that a particular base-class member can be used by the derived class, even though the derivation is private. For example, suppose you want to be able to use the valarray min() and max() methods with the Student class. In this case, in `studenti.h`, you can add using declarations to the public section:

```cpp
class Student : private std::string, private std::valarray<double>
{
...
public:
    using std::valarray<double>::min;
    using std::valarray<double>::max;
    ...
};
```

The using declaration makes the `valarray<double>::min()` and `valarray<double>::max()` methods available as if they were public Student methods:

```cpp
cout << "high score: " << ada[i].max() << endl;
```

Note that the using declaration just uses the member name—no parentheses, no function signatures, no return types. For example, to make the `valarray` `operator[]()` method available to the Student class, you’d place the following using declaration in the public section of the Student class declaration:

```cpp
using std::valarray<double>::operator[];
```

This would make both versions (const and non-const) available. You could then remove the existing prototypes and definitions for `Student::operator[]()`. The using declaration approach works only for inheritance and not for containment.

There is an older way to redeclare base-class methods in a privately derived class: You place the method name in the public section of the derived class. Here’s how you would do that:

```cpp
class Student : private std::string, private std::valarray<double>
{
public:
    std::valarray<double>::operator[];  // redeclare as public, just use name
    ...
};
```

This looks like a using declaration without the using keyword. This approach is *deprecated*, meaning that the intention is to phase it out. So if your compiler supports the using declaration, you can use it to make a method from a private base class available to the derived class.

## Multiple Inheritance

MI describes a class that has more than one immediate base class. As with single inheritance, public MI should express an *is-a* relationship. For example, if you have a `Waiter` class and a `Singer` class, you could derive a `SingingWaiter` class from the two:
