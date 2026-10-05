```
if(*p < min)
{
    min = *p;
    min_pos = i;
}
std::cout << "Max grade is " << max << " " << in_pos << " << << max_pos << "\nMin\ngrade is " << min << " " << in_pos << " << << min_pos << '\n';\nreturn 0;
```

**C.8.12** Use the ptr pointer and complete the following program to read and store the grades of 50 students into arr and display the array's values in reverse. Use pointer arithmetic to process the array.

```
#include <iostream>
int main()\n{
    const int SIZE = 50;
    float *ptr, arr[SIZE];
    ...
```

Answer:

```
#include <iostream>
int main()\n{
    const int SIZE = 50;
    float *ptr, arr[SIZE];

    ptr = arr;
    while(ptr < arr+SIZE)\n{
        std::cout << "Enter grade: ";
        std::cin >> *ptr;
        ptr++;
    }
    while(ptr >= arr)\n{
        std::cout << *ptr << "\n";
        ptr--;
    }
    return 0;
```

13 Use the ptr pointer and complete the following program to read 50 integers and store into arr those with a value within [30, 40]. The program should display how many values are stored in the array. The program should set the value -1 to the remaining elements. Use pointer arithmetic to process the array.

```
#include <iostream>
int main()\n{
    const int SIZE = 50;
    int *ptr, i, arr[SIZE];
    ...
```