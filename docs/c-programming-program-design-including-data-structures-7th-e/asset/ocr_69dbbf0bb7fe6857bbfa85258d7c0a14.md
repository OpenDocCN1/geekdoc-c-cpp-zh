The last statement, that is,

```
return 0;
```

returns the value 0 to the operating system when the program terminates. We will elaborate on this statement later in this chapter.

Before we identify various parts of a C++ program, let’s look at one more output statement. Consider the following statement:

```
cout << "7 + 8 = " << 7 + 8 << endl;
```

In this output statement, the expression "7 + 8 = " , which is a string, evaluates to itself. Let us consider the second expression, 7 + 8. This expression consists of the numbers 7 and 8, and the C++ arithmetic operator +. Therefore, the result of the expression 7 + 8 is the sum of 7 and 8, which is 15. Thus, the output of the preceding statement is:

```
7 + 8 = 15
```

In this chapter, until we explain how to properly construct a C++ program, we will be using output statements such as the preceding ones to explain various concepts. After finishing Chapter 2, you should be able to write C++ programs well enough to do some computations and show results.

Next, let us note the following about the previous C++ program. A C++ program is a collection of functions, one of which is the function main. Roughly speaking, a function is a set of statements whose objective is to accomplish something. The preceding program consists of only the function main; all C++ programs require a function main.

The first four lines of the program begins with the pair of symbols // (shown in green), which are comments. Comments are for the user; they typically explain the purpose of the programs, that is, the meaning of the statements. (We will elaborate on how to include comments in a program later in this chapter.) The next line of the program, that is,

```
#include <iostream>
```

allows us to use the (predefined object) cout to generate output and the (manipulator) endl. The statement

```
using namespace std;
```

allows you to use cout and endl without the prefix std::. It means that if you do not include this statement, then cout should be used as std::cout and endl should be used as std::endl. We will elaborate on this later in this chapter.

Next consider the following line:

```
int main()
```