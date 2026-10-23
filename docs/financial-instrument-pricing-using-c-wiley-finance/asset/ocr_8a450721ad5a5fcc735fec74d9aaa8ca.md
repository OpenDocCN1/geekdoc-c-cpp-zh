```
{
    std::string name_;
    std::string address_;
    int age_;

    Person2(int age, const std::string name, const std::string address)
        : age_(age), name_(name), address_(address) {}
};
```

We use uniform initialisation as follows:

```
// Aggregate initialisation; initialise the data in a
// struct without needing a constructor
Person p1{ "Joe", "Denver", 23 };

// ERROR! Person p1_a( "Joe", "Denver", 23 );
// (No function talking three arguments!!)

// Using constructors to initialise data
Person2 p2{ 55, "Piet", "Zurich" };
Person2 p3( 55, "Piet", "Zurich" );
```

We see from class Person that we can initialise a class’s member data using braced initialisation even though the class does not have the appropriate constructors.

# 7.3.6 Initialiser Lists

An object of type std::initializer_list<T> is a lightweight proxy object that provides access to an array of objects of type const T:

```
// Initialiser lists
template <typename T>
class ILClass
{ // Class using initialiser lists
private:
    std::vector<T> v;
public:
    ILClass(std::initializer_list<T> myList) : v(myList) {}

    void append(std::initializer_list<T> myList)
    { // Extend vector v before element at specified position

        v.insert(std::end(v), std::begin(myList),
            std::end(myList));
    }

    void print() const
    {
```