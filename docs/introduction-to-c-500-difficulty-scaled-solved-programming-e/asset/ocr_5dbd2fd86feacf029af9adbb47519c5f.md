# 16 More about Functions 505

```
double* test(double *p1, double *p2)
{
    if(*p1 < *p2)
        return p1;
    else
        return p2;
}
double& test(double& r1, double& r2)
{
    if(r1 < r2)
        return r1;
    else
        return r2;
}
```

Answer: The first version of test() returns the pointer to the parameter with the smaller value, while the second returns the reference. In the first call we have p1 = &a, so *p1 = a = 1.2. Similarly, p2 = &b, so *p2 = b = 3.4. Therefore, test() returns the pointer to a, the state-*test(&a, &b) = 5.6; which makes a equal to 5 and the program displays: 5.6 3.4
In the second call of test(), since r1 = a = 5.6 and r2 = b = 3.4, test() returns a reference to r2. Since test() returns a reference to b, b equals to 7 and the program displays: 5.6 7.8

C.16.5 Write a function template that takes three numeric values of the same generic type and returns the value of the pair with the largest sum. For example, if the values are 3, 1, 2 the function should return 5. Overload the function with another function template with a void return type, which takes as parameter an array of generic type and returns the maximum and minimum value of the array through reference parameters of generic type. Write a program that verifies the operation of the two functions.

```
#include <iostream>
```

```
const int SIZE = 5;

template <typename T> T find(T a, T b, T c);
template <typename T> void find(T arr[], T& min, T& max);

int main()
{
    int i = 3, j = 1, k = 2;
    double m, n, a[SIZE] = {5.1, 1.1, 2.1, 3.1, 4.1};

    std::cout << "Sum:" << find(i, j, k) << '\\n';
    find(a, m, n);
    std::cout << "Min:" << m << " Max:" << n << '\\n';
    return 0;
}
```

```
template <typename T> T find(T a, T b, T c)
{
    T max = a+b;
    if(max < a+c)
        max = a+c;
}
```