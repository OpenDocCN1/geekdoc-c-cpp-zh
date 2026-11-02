# REVIEW EXERCISES

**R1.1** Explain the difference between using a computer program and programming a computer.

**R1.2** Which parts of a computer can store program code? Which can store user data?

**R1.3** Which parts of a computer serve to give information to the user? Which parts take user input?

**R1.4** A toaster is a single-function device, but a computer can be programmed to carry out different tasks. Is your cell phone a single-function device, or is it a programmable computer?

**R1.5** Explain two benefits of using C++ over machine code.

**R1.6** On your own computer or on your lab computer, find the exact location (folder or directory name) of

a. The sample file hello.cpp (after you saved it in your development environment).

b. The standard header file <iostream>.

**R1.7** What does this program print?

```
```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "6 * 7 = " << 6 * 7 << endl;
    return 0;
}
```
```

**R1.8** What does this program print? Pay close attention to spaces.

```
```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "Hello" << "World" << endl;
    return 0;
}
```
```

**R1.9** What does this program print?

```
```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "Hello" << endl << "World" << endl;
    return 0;
}
```
```

**R1.10** Write three versions of the hello.cpp program that have different compile-time errors. Write a version that has a run-time error.

**R1.11** How do you discover compile-time errors? How do you discover run-time errors?

**R1.12** Write an algorithm to settle the following question: A bank account starts out with $10,000. Interest is compounded monthly at 6 percent per year (0.5 percent per month). Every month, $500 is withdrawn to meet college expenses. After how many years is the account depleted?