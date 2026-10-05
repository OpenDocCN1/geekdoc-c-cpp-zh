# 422 Introduction to C++

```
double *find_diff(const double al[], const double a2[], int size, int *items)
{
    int i, j, found;
    double *mem;

    mem = new (std::double[size]); /* It is just to see an example
with nothrow. */
    if (mem == nullptr)
    {
        cout << "Error: Not available memory\n";
        exit(EXIT_FAILURE);
    }
    for(i = 0; i < size; i++)
    {
        found = 0; /* This variable indicates whether an element of the
        first array exists in the second, or not. The value 0 means that it does not
        exist. */
        for(j = 0; j < size; j++)
        {
            if(a2[j] == al[i])
            {
                found = 1; /* Since this element exists, we stop
                searching. */
                break;
            }
            // If it does not exist, it is stored in the memory.
            if (found == 0)
            {
                mem[*items] = al[i];
                (*items)++;
            }
        }
    }
    return mem;
}
```

C.14.6 Write a program that declares an array of double pointers to strings and allocates the exact
memory needed to store strings of less than 100 characters. The program should read 20 strings and
display the longest. If more than one string is the longest, the program should display the one
first.

```
#include <iostream>
#include <cstring>
using std::cout;
using std::cin;

const int SIZE = 100;

int main()
{
    char *ptr[SIZE], str[100];
    int i, pos, max_len; /* pos is used to indicate the ptr element,
    which points to the longest string. max_len holds its length. */
    pos = max_len = 0;
```