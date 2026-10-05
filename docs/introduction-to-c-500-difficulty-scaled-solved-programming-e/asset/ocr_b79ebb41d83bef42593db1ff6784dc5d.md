# 18 • Operator Overloading 591

```
template <typename T> void sort(vector<T>& v)
{
    int i, j, size;
    T tmp; // The constructor of each class will be called;

    size = v.size();
    for(i = 0; i < size; i++)
{
        for(j = i+1; j < size; j++)
        {
            if(v[i] > v[j]) /* To compare the elements
overloaded > operator function of each class is called. */
            {
                tmp = v[i];
                v[i] = v[j];
                v[j] = tmp;
            }
        }
    }
}
```

# UNSOLVED EXERCISES

U.18.1 Modify the following program so that it is compiled and displays:

```
Begin
Show
End

#include <iostream>
using namespace std;
int main()
{
    "Show\n" << cout;
    return 0;
}
```

There is a restriction to change main(), it should remain the same.

U.18.2 Modify the Array in example C.18.5 to Safe_Arr, to dynamically create a safe array. Appropriate functions in the class so that the following program works.

```
class Safe_Arr
{
private:
    int *arr; /* This pointer should be used to allocate memory for
size integers. */
    int size; // Number of elements.
public:
    ...
};
```