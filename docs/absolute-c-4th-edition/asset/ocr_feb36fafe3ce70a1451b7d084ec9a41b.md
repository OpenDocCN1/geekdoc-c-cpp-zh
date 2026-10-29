The following creates a dynamically allocated variable of type Record and sets the member variables of the dynamic struct variable to 2001 and ’A’:

```cpp
Record *p;
p = new Record;
p->number = 2001;
p->grade = ’A’;
```

The notations

```cpp
p->grade
```

and

```cpp
(*p).grade
```

have the same meaning. However, the first is more convenient and is almost always the notation used.

# THE this POINTER

When defining member functions for a class, you sometimes want to refer to the calling object. This pointer is a predefined pointer that points to the calling object. For example, consider a class like the following:

```
```cpp
class Sample
{
public:
        ...
        void showStuff() const;
        ...
private:
        int stuff;
        ...
};
```
```

The following two ways of defining the member function showStuff are equivalent:

```
```cpp
void Sample::showStuff() const
{
    cout << stuff;
}

//Not good style, but this illustrates the this pointer:
void Sample::showStuff()
{
    cout << this->stuff;
}
```
```