# Display 19.5   Using the list Template Class

```
```cpp
//Program to demonstrate the STL template class list.
#include <iostream>
#include <list>
using std::cout;
using std::endl;
using std::list;

int main( )
{
   list<int> listObject;

   for (int i = 1; i <= 3; i++)
      listObject.push_back(i);

   cout << "List contains:\n"
   list<int>::iterator iter;
   for (iter = listObject.begin( ); iter != listObject.end( );
                                      iter++)
      cout << *iter << " ";

   cout << endl;

   cout << "Setting all entries to 0:\n"
   for (iter = listObject.begin( ); iter != listObject.end( );
                                      iter++)
      *iter = 0;

   cout << "List now contains:\n"
   for (iter = listObject.begin( ); iter != listObject.end( );
                                      iter++)
      cout << *iter << " ";
   cout << endl;

   return 0;
}
```
```

# Sample Dialogue

```
```
List contains:
1 2 3
Setting all entries to 0:
List now contains:
0 0 0
```
```