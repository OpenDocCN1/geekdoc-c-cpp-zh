+   - A map may be initialized using two iterators. The iterators may either point to `value_type` values for the map to be constructed, or to plain pair objects. If pairs are used, their first element represents the type of the keys, and their second element represents the type of the values. Example:

```
```cpp
pair<string, int> pa[] =
{
        pair<string,int>("one", 1),
        pair<string,int>("two", 2),
        pair<string,int>("three", 3),
};

map<string, int> object(&pa[0], &pa[3]);
```
```

In this example, `map<string, int>::value_type` could have been written instead of `pair<string, int>` as well.

If `begin` represents the first iterator that is used to construct a map and if `end` represents the second iterator, `[begin, end)` will be used to initialize the map. Map may be contrary to intuition, the map constructor only enters *new* keys. If the last element of `pa` would have been "one", 3, only two elements would have entered the map: the "one", 1 and "two", 2. The value "one", 3 would silently have been ignored.

The map receives its own copies of the data to which the iterators point as illustrated by the following example:

```
```cpp
#include <iostream>
#include <map>
using namespace std;

class MyClass
{
public:
    MyClass()
    {
        cout << "MyClass constructor\n";
    }
    MyClass(MyClass const &other)
    {
        cout << "MyClass copy constructor\n";
    }
    ~MyClass()
    {
        cout << "MyClass destructor\n";
    }
};

int main()
{
    pair<string, MyClass> pairs[] =
    {
        pair<string, MyClass>("one", MyClass())
    };
    cout << "pairs constructed\n";

    map<string, MyClass> mapsm(&pairs[0], &pairs[1]);
    cout << "mapsm constructed\n";
}
/*
    Generated output:
MyClass constructor
```
```