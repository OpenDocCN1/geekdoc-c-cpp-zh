
```cpp
HasFriend<int> hfi1(10);
cout << "After hfi1 declared: ";
counts();
HasFriend<int> hfi2(20);
cout << "After hfi2 declared: ";
counts();
HasFriend<double> hfdb(10.5);
cout << "After hfdb declared: ";
counts();
report(hfi1);
report(hfi2);
report(hfdb);

return 0;
}
```

Some compilers will warn about using a non-template friend. Here is the output of the program in Listing 14.22:

```text
No objects declared: int count: 0; double count: 0
After hfi1 declared: int count: 1; double count: 0
After hfi2 declared: int count: 2; double count: 0
After hfdb declared: int count: 2; double count: 1
HasFriend<int>: 10
HasFriend<int>: 20
HasFriend<double>: 10.5
```

## Bound Template Friend Functions to Template Classes

You can modify the preceding example by making the friend functions templates themselves. In particular, you can set things up for bound template friends, so each specialization of a class gets a matching specialization for a friend. The technique is a bit more complex than for non-template friends and involves three steps.

For the first step, you declare each template function before the class definition:

```cpp
template <typename T> void counts();
template <typename T> void report(T &);
```

Next, you declare the templates again as friends inside the function. These statements declare specializations based on the class template parameter type:

```cpp
template <typename TT>
class HasFriendT
{
...
    friend void counts<TT>();
    friend void report<>(HasFriendT<TT> &);
};
```

The `<>` in the declarations identifies these as template specializations. In the case of `report()`, the `<>` can be left empty because the following template type argument can be deduced from the function argument:

```cpp
HasFriend<TT>
```

You could, however, use this instead:

```cpp
report<HasFriend<TT> >(HasFriend<TT> &)
```

However, the `counts()` function has no parameters, so you have to use the template argument syntax (`<TT>`) to indicate its specialization. Note, too, that `TT` is the parameter type for the `HasFriend` class.

Again, the best way to understand these declarations is to imagine what they become when you declare an object of a particular specialization. For example, suppose you declare this object:

```cpp
HasFriend<int> squack;
```

Then the compiler substitutes `int` for `TT` and generates the following class definition:

```cpp
class HasFriend<int>
{
...
    friend void counts<int>();
    friend void report<HasFriend<int> >(HasFriend<int> &);
};
```

One specialization is based on `TT`, which becomes `int`, and the other is based on `HasFriend<TT>`, which becomes `HasFriend<int>`. Thus, the template specializations `counts<int>()` and `report<HasFriend<int> >()` are declared as friends to the `HasFriend<int>` class.

The third requirement the program must meet is to provide template definitions for the friends. Listing 14.23 illustrates these three aspects. Note that Listing 14.22 has one `counts()` function that is a friend to all `HasFriend` classes, whereas Listing 14.23 has two `counts()` functions, one of which is a friend to each of the instantiated class types. Because the `counts()` function calls have no function parameter from which the compiler can deduce the desired specialization, these calls use the `counts<int>()` and `counts<double>()` forms to indicate the specialization. For the calls to `report()`, however, the compiler can use the argument type to deduce the specialization. You could use the `<>` form to the same effect:

```cpp
report<HasFriend<int> >(&hf2i);  // same as report(&hf2i);
```

### Listing 14.23 `tmp2tmp.cpp`

```cpp
// tmp2tmp.cpp -- template friends to a template class
#include <iostream>
using std::cout;
using std::endl;

// template prototypes
template <typename T> void counts();
template <typename T> void report(T &);

// template class
template <typename TT>
class HasFriendT
{
private:
    TT item;
    static int ct;
public:
    HasFriendT(const TT & i) : item(i) {ct++;}
    ~HasFriendT() { --ct; }
    friend void counts<TT>();
    friend void report<>(HasFriendT<TT> &);
};

template <typename T>
int HasFriendT<T>::ct = 0;

// template friend functions definitions
template <typename T>
void counts()
{
    cout << "template size: " << sizeof(HasFriendT<T>) << "; ";
    cout << "template counts(): " << HasFriendT<T>::ct << endl;
}

template <typename T>
void report(HasFriendT<T> & hf)
{
    cout << hf.item << endl;
}

int main()
{
    counts<int>();
    HasFriendT<int> hfi(10);
    HasFriendT<int> hfi2(20);
    HasFriendT<double> hfdb(10.5);
    report(hfi);   // generate report(HasFriendT<int> &)
    report(hfi2);  // generate report(HasFriendT<int> &)
    report(hfdb);  // generate report(HasFriendT<double> &)
    cout << "counts<int>() output:\n";
    counts<int>();
    cout << "counts<double>() output:\n";
    counts<double>();

    return 0;
}
```

Here is the output of the program in Listing 14.23:

```text
template size: 4; template counts(): 0
10
20
10.5
counts<int>() output:
template size: 4; template counts(): 2
counts<double>() output:
template size: 8; template counts(): 1
```

As you can see, `counts<double>()` reports a different template size from `counts<int>()`, demonstrating that each T type now gets its own `counts()` friend.

## Unbound Template Friend Functions to Template Classes

The bound template friend functions in the preceding section are template specializations of a template declared outside a class. An int class specialization gets an int function specialization, and so on. By declaring a template inside a class, you can create unbound friend functions for which every function specialization is a friend to every class specialization. For unbound friends, the friend template type parameters are different from the template class type parameters:

```cpp
template <typename T>
class ManyFriend
{
...
    template <typename C, typename D> friend void show2(C &, D &);
};
```

Listing 14.24 shows an example that uses an unbound friend. In it, the function call `show2(hfi1, hfi2)` gets matched to the following specialization:

```cpp
void show2<ManyFriend<int> &, ManyFriend<int> &>
        (ManyFriend<int> & c, ManyFriend<int> & d);
```

Because it is a friend to all specializations of ManyFriend, this function has access to the item members of all specializations. But it only uses access to `ManyFriend<int>` objects.

Similarly, `show2(hfdb, hfi2)` gets matched to this specialization:

```cpp
void show2<ManyFriend<double> &, ManyFriend<int> &>
        (ManyFriend<double> & c, ManyFriend<int> & d);
```

It, too, is a friend to all ManyFriend specializations, and it uses its access to the item member of a `ManyFriend<int>` object and to the item member of a `ManyFriend<double>` object.

### Listing 14.24 `manyfrnd.cpp`

```cpp
// manyfrnd.cpp -- unbound template friend to a template class
#include <iostream>
using std::cout;
using std::endl;

template <typename T>
class ManyFriend
{
private:
    T item;
public:
    ManyFriend(const T & i) : item(i) {}
    template <typename C, typename D> friend void show2(C &, D &);
};

template <typename C, typename D> void show2(C & c, D & d)
{
    cout << c.item << ", " << d.item << endl;
}

int main()
{
    ManyFriend<int> hfi1(10);
    ManyFriend<int> hfi2(20);
    ManyFriend<double> hfdb(10.5);
    cout << "hfi1, hfi2: ";
    show2(hfi1, hfi2);
    cout << "hfdb, hfi2: ";
    show2(hfdb, hfi2);

    return 0;
}
```

Here's the output of the program in Listing 14.24:

```text
hfi1, hfi2: 10, 20
hfdb, hfi2: 10.5, 20
```

## Template Aliases (C++11)

It can be convenient, especially in template design, to create aliases for types. You can use typedef to create aliases for template specializations:

```cpp
// define three typedef aliases
typedef std::array<double, 12> arrd;
typedef std::array<int, 12> arri;
typedef std::array<std::string, 12> arrst;
arrd gallons; // gallons is type std::array<double, 12>
arri days;    // days is type std::array<int, 12>
arrst months; // months is type std::array<std::string, 12>
```

But if you find yourself writing code similar to the preceding typedefs, over and over, you might wonder if you've forgotten some language feature that simplifies the task or if the language has forgotten to supply such a feature. In this case, C++11 provides a feature previously missing—a way to use a template to provide a family of aliases. Here's what the approach looks like:

```cpp
template<typename T>
    using arrtype = std::array<T,12>;   // template to create multiple aliases
```

This makes `arrtype` a template alias that can be used as a type, as follows:

```cpp
arrtype<double> gallons;    // gallons is type std::array<double, 12>
arrtype<int> days;          // days is type std::array<int, 12>
arrtype<std::string> months; // months is type std::array<std::string, 12>
```

In short, `arrtype<T>` means type `std::array<T,12>`.

C++11 extends the `using =` syntax to non-templates too. In that case, it becomes equivalent to an ordinary typedef:

```cpp
typedef const char * pc1;       // typedef syntax
using pc2 = const char *;       // using = syntax
typedef const int *(*pa1)[10];  // typedef syntax
using pa2 = const int *(*)[10]; // using = syntax
```

As you get used to it, you may find the new form more readable because it separates the type name from type information more clearly.

Another C++11 addition to templates is the *variadic template*, which allows you to define a template class or function that can take a variable number of initializers. Chapter 18, “Visiting with the New C++ Standard,” looks into this topic.

## Summary

C++ provides several means for reusing code. Public inheritance, described in Chapter 13, “Class Inheritance,” enables you to model *is-a* relationships, with derived classes being able to reuse the code of base classes. Private and protected inheritance also let you reuse base-class code, this time modeling *has-a* relationships. With private inheritance, public
