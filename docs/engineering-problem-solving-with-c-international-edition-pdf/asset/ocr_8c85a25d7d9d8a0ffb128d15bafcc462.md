| Method Name | Method Description |
| :--- | :--- |
| back() | Return the value of the last element. |
| begin() | Return iterator to first element. |
| capacity() | Return the capacity. |
| empty() | Return true if size is zero. Return false otherwise. |
| end() | Return iterator to one past last element. |
| erase() | Delete element. |
| insert() | Insert element. |
| pop_back() | Delete last element. |
| push_back() | Add element to the end. |
| resize() | Change the capacity. |
| size() | Return the size. |

Notice the syntax used to specify the type of data that each vector will store. The use of vector<data type> is required because vector is defined as a class template. Templates defined in the STL support generic programming by implementing the concept of a type without specifying the specific type of data that will be stored. For example, the concept of a vector, or an array, is a container that stores a sequential block of data. Data can be added to, or deleted from, the end of a vector very efficiently, and a vector, like an array, supports random access of data, using offsets. Since these concepts are independent of the data, a template for a vector is defined and the compiler generates a concrete instance of the template when a vector is declared with a specific type.

The following example illustrates the use of the vector class and the difference between the size and the capacity of a vector. Notice that we must include the header file vector. Because vector is part of the Standard C++ Library, the linking occurs automatically.

```
/*-------------------------------------------------------------*/
/* Program chapter7_10                                         */
/*-------------------------------------------------------------*/
#include<iostream>    //Required for cout
#include<vector>      //Required for vector
using namespace std;
int main()
{
   //Declare and initialize objects.
   vector<int> v(5);
   //Print the capacity and the size.
   cout << "Capacity: " << v.capacity() << " Size: " << v.size()
        << endl;
```