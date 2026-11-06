
```cpp
{
    ForEach(iterator, Vector2<Type>, std::vector<Type> >
        (this->begin(), this->end(), *this, &Vector2<Type>::rows);
}

template <typename Type>
void Vector2<Type>::rows(std::vector<Type> &row)
{
    ForEach(row.begin(), row.end(), *this,
                         &Vector2<Type>::columns);
    std::cout << '\n';
}

template <typename Type>
void Vector2<Type>::columns(Type &str)
{
    std::cout << str << " ";
}

using namespace std;

int main()
{
    Vector2<string> c;
    c.push_back(vector<string>(3, "Hello"));
    c.push_back(vector<string>(2, "World"));

    c.process();
}
/*
    Generated output:

    Hello Hello Hello
    World World
*/
```

- Analogously, a full class template may be declared as friend. This allows all instantiations of the friend’s member functions to instantiate objects of the class template declaring the friend class. In this case, the class declaring the friend should offer functionality that is useful to different instantiations of its friend class (i.e., instantiations using different template arguments). The syntactic convention is comparable to the convention used when declaring an unbound friend function template:

```cpp
template <typename Type>
class PtrVector
{
    template <typename Iterator, typename Class>
    friend class Wrapper;      // unbound friend class
};
```

All members of the class template Wrapper may now instantiate PtrVectors using any actual type for its Type parameter. This allows the Wrapper instantiation to access all of PtrVector’s private members.

- When only some members of a class template need access to private members of another class template (e.g., the other class template has private constructors and only some members of the first class template need to instantiate objects of the second class template), then the latter class template may declare only those members of the former class template requiring access to its private members as its friends. Again, the friend class’s interface may be left unspecified. However, the compiler must be informed that the friend member’s class is indeed a class. A forward declaration of that class must therefore be provided. In the next example `PtrVector` declares `Wrapper::begin` as its friend. Note the forward declaration of the class `Wrapper`:

```cpp
    template <typename Iterator>
    class Wrapper;

    template <typename Type>
    class PtrVector
    {
        template <typename Iterator> friend
            PtrVector<Type> Wrapper<Iterator>::begin(Iterator const &t1);
        ...
    };
```

### 21.10.4 Extended friend declarations (C++11, 4.7)

The C++11 standard defines extended friend declarations. Extended friend declarations are also available for class templates.

Extended friend declarations for class templates allow us to use template type parameters as friend declarations. A template type argument, however, does not necessarily have to be a type for which the keyword `friend` makes sense, like `int`. In those cases the friend declaration is simply ignored.

Consider the following class template, declaring `Friend` as a friend:

```cpp
    template <typename Friend>
    class Class
    {
        friend Friend;
        void msg();                 // private, displays some message
    };
```

Now, an actual `Friend` class may access all of `Class`'s members

```cpp
    class Concrete
    {
        Class<Concrete> d_class;
        Class<std::string> d_string;

    public:
        void msg()
        {
            d_class.msg();      // OK: calls private Class<Concrete>::msg()
            //d_string.msg(); // fails to compile: msg() is private
        }
    };
```

A declaration like `Class<int> intClass` is also OK, but here the friend declaration is simply ignored. After all, there are no 'int members' to access `Class<int>`'s private members.

## 21.11 Class template derivation

Class templates can be used for inheritance purposes as well. When a class template is used in class derivation, the following situations should be distinguished:

- An existing class template is used as base class when deriving an ordinary class. The derived class itself will partially be a class template, but this is somewhat hidden from view when an object of the derived class is defined.
- An existing class template is used as the base class when deriving another class template. Here the class template characteristics remain clearly visible.
- An ordinary class is used as the base class when deriving a template class. This interesting hybrid allows us to construct class templates that are *partially compiled*.

These three variants of class template derivation are elaborated in this and the upcoming sections.

Consider the following base class:

```cpp
template<typename T>
class Base
{
    T const &t;

    public:
        Base(T const &t);
};
```

The above class is a class template that can be used as a base class for the following derived class template Derived:

```cpp
template<typename T>
class Derived: public Base<T>
{
    public:
        Derived(T const &t);
};
template<typename T>
Derived<T>::Derived(T const &t)
:
    Base(t)
{}
```

Other combinations are also possible. The base class may be instantiated by specifying template arguments, turning the derived class into an ordinary class (showing a class object's definition as well):

```cpp
class Ordinary: public Base<int>
{
    public:
        Ordinary(int x);
};
inline Ordinary::Ordinary(int x)
:
    Base(x)
{}

    Ordinary ordinary(5);
```

This approach allows us to add functionality to a class template, without the need for constructing a derived class template.

Class template derivation pretty much follows the same rules as ordinary class derivation, not involving class templates. Some subtleties that are specific for class template derivation may easily cause

```cpp
void (Handler::*)(std::string const &cmd)>
(s_cmds, s_cmds_end)
{
}
```

- The member process iterates along the map’s elements. Once the first word on the command line matches the initial characters of the command, the corresponding command is executed. If no such command is found, an error message is issued:

```cpp
void Handler::process(std::string const &line)
{
    istringstream istr(line);
    string cmd;
    istr >> cmd;
    for (iterator it = begin(); it != end(); it++)
    {
        if (it->first.find(cmd) == 0)
        {
            (this->*it->second)(line);
            return;
        }
    }
    cout << "Unknown command: " << line << '\n';
}
```

### 21.11.2 Deriving class templates from class templates

Although it’s perfectly acceptable to derive an ordinary class from a class template, the resulting class of course has limited generality compared to its template base class. If generality is important, it’s probably a better idea to derive a class template from a class template. This allows us to extend an existing class template with new functionality or to override the functionality of the existing class template.

The class template `SortVector` presented below is derived from the existing class template `std::vector`. It allows us to perform a *hierarchic sort* of its elements using any ordering of any data members its data elements may contain. To accomplish this there is but one requirement. `SortVector`’s data type must offer dedicated member functions comparing its members.

For example, if `SortVector`’s data type is an object of class `MultiData`, then `MultiData` should implement member functions having the following prototypes for each of its data members which can be compared:

```cpp
bool (MultiData::*)(MultiData const &rhv)
```

So, if `MultiData` has two data members, `int d_value` and `std::string d_text` and both may be used by a hierarchic sort, then `MultiData` should offer the following two members:

```cpp
bool intCmp(MultiData const &rhv);  // returns d_value < rhv.d_value
bool textCmp(MultiData const &rhv); // returns d_text < rhv.d_text
```

Furthermore, as a convenience it is assumed that operator<< and operator>> have been defined for `MultiData` objects.

The class template `SortVector` is directly derived from the template class `std::vector`. Our implementation inherits all members from that base class. It also offers two simple constructors:

```cpp
template <typename Type>
class SortVector: public std::vector<Type>
```
