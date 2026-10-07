# Dynamic Memory Allocation

As discussed in Chapter 10, when declaring an array, the size declarator must be either a literal or a constant, not a variable. The following program from Chapter 10 attempts, unsuccessfully, to use a variable numTests in declaring the size of an array:

```
#include <iostream>
using namespace std;
int main()
{
    int numTests;
    cout << "Enter the number of test scores:";
    cin >> numTests;
    int testScore[numTests];
    return 0;
}
```

The result is a compiler error. The compiler will flag the declaration of the array (int testScore[numTests]) and complain that a constant was expected. The reason a constant (or literal) expression is required is in this program we are allocating memory for the array at compile time. The compiler needs to know exactly how much memory to allocate. However, if a variable is the size declarator, the compiler does not know how much memory to allocate because a variable's value may change. Indeed, in the preceding example, the value of the variable used as the size declarator is not even known until runtime.

Having said though, it is often desirable to have the user determine at runtime the size of the array so that it is neither too small nor too large, but just right. To accomplish this, you need to declare the array using dynamic memory allocation. The following program modifies the previous one to use dynamic memory allocation:

```
#include <iostream>
using namespace std;
int main()
{
    int numTests;
    cout << "Enter the number of test scores:";
    cin >> numTests;
    int * iPtr = new int[numTests];
    for (int i = 0; i < numTests; i++)
    {
        cout << "Enter test score #" << i + 1 << " : ";
        cin >> iPtr[i];
    }
    for (i = 0; i < numTests; i++)
        cout << "Test score #" << i + 1 << " is "
        << iPtr[i] << endl;
    delete[] iPtr;
    return 0;
}
```

Some sample input and output follows:
nEnter the number of test scores: 3
Enter test score #1: 66