# 502 Introduction to C++

Before we continue with the exercises I'd like to remind you something that I had written in Chapter I, yes, that was hard enough to pay attention. Now that we have come a long way and things are getting harder and harder (this chapter was really difficult), I think you will give it the proper attention. In addition to error messages, the compiler may issue warnings to the programmer about potential malfunction of the program. Although a program that issues only warning messages can be compiled, always check them and fix them if needed in order to avoid problematic situations. In fact, for better control of your program and greater security, I suggest that you set the warning level at the maximum level supported by your compiler in order to catch all of them.

# EXERCISES

**C.16.1** What is the output of the following program?

```
#include <iostream>

void test(int *p, int &r, int a = 2);

int main() {
    int i = 10, j = 50;

    test(&i, j);
    std::cout << i << ' ' << j << '\n';
    return 0;
}

void test(int *p, int &r, int a) {
    *p = r;
    p = &r;
    r += 20;
}
```

**Answer:** When test() is called we p = &i and r = j. So, the *p = r; makes i equal to 50. Then, p points to j, and the *p = a; makes j equal to the default value of a, that is, 2. Finally, j is increased and becomes 22. As a result, the program displays 50. 22.

**C.16.2** Define the structure type Student with member name and grade. Write a function that has parameters two constant references to string objects and returns a reference to the larger one. Overload the function with another function, which takes as parameters two constant references to Student types and returns the name of the student with the better grade. Check if they are the same. Write a program that verifies the operation of the two functions.

```
#include <iostream>
#include <string>
using std::cout;
using std::string;
```