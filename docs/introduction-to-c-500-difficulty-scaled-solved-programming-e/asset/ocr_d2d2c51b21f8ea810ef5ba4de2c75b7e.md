# Default Functions

Until now, we've learned the functions that the compiler provides by default for a class T

+   a. The default constructor: T().
b. The default copy assignment operator, which is a function declared as:
T& operator=(const T&). For example, we'll see in Chapter 18, when we write t1 = t2;
  operator= function is called, which copies the values of the non-static members of nt2 to t1. If the member is an array, its elements are copied. The function returns a reference to the left operand.
c. The default destructor: ~T().

These are the functions that the compiler will generate for you and by default, unless you've defined your own versions. Notice in Chapter 19 there are some special cases where the compiler does not create the default functions. The general rule is that if a class has a member by definition cannot be constructed, copied, or destroyed, then the compiler deletes it, as we'll see in Chapter 19, the corresponding default function. For example, if the class contains a reference or const member, the compiler does not generate the copy assignment operator. See the following code and read the comments:

```
class T
{
    const int r;
    T(int i) : r(i) {} /* r becomes equal to i. We'll see this syntax in */
};
```

```
t1(10), t2(20); // Compilation error, because the copy assignment operator is deleted. If you want to make the copy, you'll need to define your own copy function, as you'll learn in Ch.18. */
```

It makes sense for the compiler to delete the copy function, since it is not allowed to change a const variable. Let's have a short test, find the errors in the following program:

```
#include <iostream> // Example 17.8
#include <cstring>
```

```
class T
private:
    char str[5];
    T(int i, int j) {a=i; b=j;}
public:
    int a, b;
    T() {}
    T(char s[], int i = 0) {strcpy(str, s); a=b=i;}
~T(int i) {std::cout << "Out\n";}
}
```

```
int main()
{
    t1(10), t2(20), t3("Find the errors\n", t4(10, 20);
    return 0;
}
```