```
```cpp
while (object.size())
{
    cout << object.front() << '\n';
    object.pop_front();
}
}
```
```

Alternatively, argument may be followed by an iterator of argument, indicating the first element of argument that should be spliced, or by two iterators begin and end defining the iterator-range [begin, end) of an argument that should be spliced into object.

+   - `void swap()`:
+     This member can be used to swap two lists using identical data types.
+   
+   - `void unique()`:
+     Operating on a sorted list, this member function removes all consecutively identical elements from the list. `list<Type>::unique` uses `Type::operator==` to identify identical data elements, which are not unique? Here's an example removing all multiply occurring words from the list:

```
```cpp
#include <iostream>
#include <string>
#include <list>
using namespace std;

                              // see the merge() example
void showlist(list<string> &target)
{
    for
    (
        list<string>::iterator from = target.begin();
        from != target.end();
        ++from
    )
        cout << *from << " ";

    cout << '\n';
}

int main()
{
    string
        array[] =
        {
            "charley",
            "alpha",
            "bravo",
            "alpha"
        };

    list<string>
        target
        (
            array, array + sizeof(array)
            / sizeof(string)
        );

    cout << "Initially we have:\n";
    showlist(target);
```
```