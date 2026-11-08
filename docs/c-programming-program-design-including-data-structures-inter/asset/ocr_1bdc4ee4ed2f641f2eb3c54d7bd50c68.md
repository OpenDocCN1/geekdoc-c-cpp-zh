5. Suppose that the enum `courseType` as defined in Exercise 2. Write a C++ function that can be used to input a value in a variable of type `courseType`.

6. Suppose that the enum `courseType` as defined in Exercise 2. Write a C++ function that can be used to output the value of a variable of type `courseType`.

7. What are some of the drawbacks of an anonymous type?

8. Define an enumeration type `triangleType` with values `EQUILATERAL`, `RIGHT`, `ISOSCELES`, and `SCALENE`. Also declare the variable `triangle` of type `triangleType` while defining this type.

9. What is wrong with the following program?

```
```cpp
#include <iostream>                         //Line 1

namespace std;                              //Line 2

int main()                                  //Line 3
{
    cout << "*$*" << endl;                  //Line 4

    return 0;                                //Line 6
}                                            //Line 7
```
```

10. What is wrong with the following program?

```
```cpp
#include <iostream.h>                       //Line 1

int main()                                  //Line 2
{
    int num = 5;                             //Line 4
    std::cout << "num = " << num << endl;   //Line 5
    return 0;                                //Line 6
}                                            //Line 7
```
```

11. What is wrong with the following program?

```
```cpp
#include <iostream>                         //Line 1

using namespace std;                         //Line 2

int main()                                  //Line 3
{
    int x;                                    //Line 5

    std::cin >> x;                            //Line 6
    cout << "x = " << x << endl;             //Line 7

    return 0;                                //Line 8
}                                            //Line 9
```
```