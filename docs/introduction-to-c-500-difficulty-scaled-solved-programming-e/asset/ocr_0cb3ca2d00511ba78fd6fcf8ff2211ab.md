# C2.35 Add appropriate functions in the class template so that the following program works. The purpose of the program is to sort the size elements contained in the memory that the p pointer points according to the bubble algorithm. To implement the bubble_sort() use the code of C.12.10.

```
#include <iostream>
```

```
template <typename T> class Sort_Arr
{
private:
    int size;
    T *p;
public:
    void bubble_sort(); // Sort the elements.
    void show() const; // Display the elements.
};
int main()
{
    Sort_Arr<int> sa_1(5); /* The constructor should be called, the size should become 5 and memory for size numbers should be allocated. The p pointer should point to that memory. The user should enter the values of the elements. */
    Sort_Arr<int> sa_2, sa_3;
    sa_3 = sa_2 = sa_1;
    sa_3.bubble_sort();
    sa_3.show();
    Sort_Arr<double> sa_4(5);
    Sort_Arr<double> sa_5(sa_4); /* The copy constructor should be called. */
    sa_5.bubble_sort();
    sa_5.show();
    sa_5[10] = 1.2; /* If the index is out of bounds, as in this case, the out_of_range exception should be thrown. */
    return 0;
}
```

Answer:

```
#include <iostream>
#include <string>
#include <stdexcept>
```

```
template <typename T> class Sort_Arr
{
private:
    int size;
    T *p;
public:
    Sort_Arr();
    Sort_Arr(int s);
    ~Sort_Arr();
    Sort_Arr(const Sort_Arr& s);
    Sort_Arr& operator=(const Sort_Arr& t);
```