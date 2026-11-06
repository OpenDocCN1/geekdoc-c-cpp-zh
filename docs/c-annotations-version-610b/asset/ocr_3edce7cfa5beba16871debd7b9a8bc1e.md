```
```cpp
{
    list<string> object;

    object.push_back(string("Hello"));
    object.push_back(string("World"));
    object.push_back(string("Hello"));
    object.push_back(string("World"));

    object.remove(string("Hello"));

    while (object.size())
    {
        cout << object.front() << '\n';
        object.pop_front();
    }
}
/*
    Generated output:
    World
    World
*/
```
```

+   - `list::reverse_iterator rend();`  
+     this member returns an iterator pointing before the first element in the list.
+   - `size_t size();`  
+     this member returns the number of elements in the list.
+   - `void reverse();`  
+     this member reverses the order of the elements in the list. The element back becomes front and vice versa.
+   - `void sort();`  
+     this member sorts the list. Once the list has been sorted, an example of its use is given at the description of the unique member function below. `list<Type>::sort` uses `Type::operator<` to sort the data in the list, which operator must therefore be available.
+   - `void splice(pos, object);`  
+     this member function transfers the contents of object to the current list, starting the insertion at the iterator position pos of the object using the splice member. Following splice, object is empty. For example:

```
```cpp
#include <iostream>
#include <string>
#include <list>
using namespace std;

int main()
{
    list<string> object;

    object.push_front(string("Hello"));
    object.push_back(string("World"));

    list<string> argument(object);

    object.splice(++object.begin(), argument);

    cout << "Object contains " << object.size() << " elements, " <<
         "Argument contains " << argument.size() <<
         " elements,\n";
```
```