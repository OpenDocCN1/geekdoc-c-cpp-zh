# 192 Introduction to C++

C.8.16 Use the pl and p2 pointers and complete the following program to read the codes of 100 products and store them into arr. The program will store a code in the array only if it is not already stored. For the users -1, the insertion of codes should terminate. The program should display the codes of the stored products, before it terminates. Use pointer arithmetic to process the array.

```
#include <iostream>
int main()
{
    const int SIZE = 100;
    int *pl1, *p2, arr[SIZE];

}
```

Answer:

```
#include <iostream>
using std::cout;
using std::cin;
```

```
int main()
{
    const int SIZE = 100;
    int *pl1, *p2, arr[SIZE];

    pl = arr;
    while (pl < arr+SIZE)
    {
        cout << "Enter code " << pl-arr+1 << ": ";
        cin >> *pl1;
        if(*pl1 == -1)
            break;
    }

    for(p2 = arr; p2 < p1; p2++) /* Traverse the array to check if the input code is already stored. */
    {
        if(*pl1 == *p2)
        {
            cout << "Error: Code " << *pl1 << " exists " << '\n';
            break;
        }
        // If the code is not stored, increase the pointer.
        if(p2 == p1)
            p1++;
    }
    // Display the codes.
    for(p2 = arr; p2 < p1; p2++)
        cout << "C:" << *p2 << '\n';
    return 0;

}
```