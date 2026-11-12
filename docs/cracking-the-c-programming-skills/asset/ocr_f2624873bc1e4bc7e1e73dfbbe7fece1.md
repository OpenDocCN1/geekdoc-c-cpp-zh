+   (c) Error
+   (d) None of the above

**Answer:** (a) Prints Both objects are not same.

+   39. Say True or False. When we declare an overload function for `==`, compiler automatically inserts one function for `!=` (L2)
+   (a) True  (b) False

**Answer:** (b) False

+   40. Identify the output of the following code. (L2)

```
#include<iostream>
using namespace std;
class IntArray
{
private:
  int privateArray[10];
public:
  int& operator[] (const int index);
};
int& IntArray::operator[] (const int index)
{
  return privateArray[index];
}
int main()
{
  IntArray array;
  array[1] == 100; // set a value
  std::cout << array[1]; // get a value
  return 0;
}
```

+   (a) Error as the array is privately scoped in class
+   (b) Prints 100
+   (c) Prints junk
+   (d) Program hangs

**Answer:** (b) Prints 100, the program overloads the subscript operator to assign value to the privately scoped array and to get the set value.