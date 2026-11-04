# More Features

So far, we've made a brief review of how C++ supports the basic concepts of object-oriented programming. Certainly, there are plenty of extra C++ features not covered in this introductory chapter. When you feel confident working with C, go to the next level, buy a C++ book, and discover them. In this section we'll introduce you to some of them, the new and delete operators, the reference variables, and the exceptions.

# The new and delete Operators

Although we may still use standard C functions (e.g., malloc()) to allocate memory dynamically, a better practice is to use the new operator. The delete operator is used to free memory. Notice that new and delete are operators, not functions. On success, new returns a pointer to the allocated memory. We may handle that pointer as we did in the past. For example, the following program allocates memory to read an integer and displays that integer:

```
```cpp
#include <iostream>
using namespace std;

int main()
{
    int *ptr;

    try
    {
        ptr = new int; // Allocate memory.
    }
    catch (bad_alloc)
    {
        cout << "Unavailable memory\n";
        exit(1);
    }
    cout << "Input: ";
    cin >> *ptr;
    cout << "Output: " << *ptr << endl;

    delete ptr; // Free memory.
    return 0;
}
```
```

If new fails, it throws the bad_alloc standard exception. Otherwise, the input number will be stored into the memory that ptr points to. We'll talk about exceptions and the try and catch keywords in a short.

To allocate memory for an array, we use the operator new[] and write the number of the elements inside the brackets. To free that memory, we use the operator delete[]. For example, to allocate and free memory for 100 float numbers, we write:

```
```cpp
float *ptr = new float[100];
delete[] ptr;
```
```

Let's see an example of how to allocate memory for some objects. The following program reads a number of students and allocates memory to read and store their data. Also, the