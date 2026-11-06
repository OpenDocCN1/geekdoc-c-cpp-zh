the remaining elements. Here is how the array is going to look in the memory:

**numbers**

| Index --> | 0 | 1 | 2 | 3 | 4 |
| --- | --- | --- | --- | --- | --- |
|  | 10 | 57 | 82 | 600 | 425 |
| Memory --> | 2000 | 2004 | 2008 | 2012 | 2016 |

The array variable `numbers` will hold the address of the first element which is `2000`. (`numbers + 1`) will give the address of the second element which is `2004` and so on. We have seen many examples of how to access the elements of an array using the access operator ( `[ ]` ). Now, we will see how to access the elements of an array using pointers. If the array variable `numbers` is holding the address of the first element, using the value at address method, `*numbers` should return the value at location `2000`, which is `10`; `*( numbers + 1 )` should return `57` and so on. Accessing the array elements with the statement `numbers [ n ]` is the same as `*( numbers + n )`.

Here is a C++ program that demonstrates the method of accessing an array using pointers:

```
```cpp
using namespace std;
main ()
{
```
```