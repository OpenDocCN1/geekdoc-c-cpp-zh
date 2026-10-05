# 208 Introduction to C++

```
int find_val(const vector<int>& v, int (*op)(int a, int b))
{
    int i, res;

    res = v[0];
    for(i = 1; i < v.size(); i++)
    {
        if(op(v[i], res))
            res = v[i];
    }
    return res;
n
```

```
int max_val(int a, int b)
{
    return a > b;
}
```

```
int min_val(int a, int b)
{
    return a < b;
}
```

In each call of find_val() the address of the respective function is passed and op points to that address. The program outputs the maximum and minimum value of the vector elements, that is, 12 and -5. As you see, find_val() works in a generic way, in the sense that the same function supports both operations. The function can be more generic and work for different types of data (i.e., not only for int), as you'll see when you learn about generic programming and function templates in Chapter 16. Instead of passing a function pointer we can pass a function object or a lambda expression, as we'll see in Chapter 26.

# ARRAY OF POINTERS TO FUNCTIONS

An array of pointers to functions is nothing more than an array whose elements are function pointers. Notice that all functions will have the same prototype. For example, the statement:

```
void (*ptr[20])(int a);
```

declares an array of 20 elements, where each element is a pointer to a function that takes an integer parameter and returns nothing. In the following program, each element of the array ptr is a pointer to a function, which takes two parameters and returns an integer.

```
#include <iostream> // Example 8.27

int f1(int a, int b);
int f2(int a, int b);
int f3(int a, int b);

int main()
{
    int (*ptr[3])(int a, int b);
    int i, j, k;
```