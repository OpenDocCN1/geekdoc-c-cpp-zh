Because an accessor function only accesses the values of the member variables, as a safeguard, we typically include the reserved word *const* at the end of the headings of these functions. Moreover, a constant member function of a class cannot modify the member variables of that class. For example, see the headings of the member functions getTime, printTime, and equalTime of the class clockType.

A member function of a class is called a **constant function** if its heading contains the reserved word const at the end. For example, the member functions getTime, printTime, and equalTime of the **class clockType** are constant functions. A constant member function of a class cannot modify the member variables of that class, so these are accessor functions. One thing that should be remembered about constant member functions is that a constant member function of a class can *only* call other constant member functions of that class. Therefore, you should be careful when you make a member function constant.

Example 10-2 shows how to use the **class clockType** in a program. Note that we have combined the definition of the class, the definition of the member functions, and the main function to create a complete program. Later in this chapter, you will learn how to separate the definition of the **class clockType**, the definitions of the member functions, and the main program, using three files.

# EXAMPLE 10-2

```
```cpp
//The program listing of the program that defines
//and uses the class clockType

#include <iostream>
using namespace std;

class clockType
{
public:
    void setTime(int, int, int);
    void getTime(int&, int&, int&) const;
    void printTime() const;
    void incrementSeconds();
    void incrementMinutes();
    void incrementHours();
    bool equalTime(const clockType&) const;

private:
    int hr;
    int min;
    int sec;
};

int main()
{
    clockType myClock;
    clockType yourClock;
```
```

1
0