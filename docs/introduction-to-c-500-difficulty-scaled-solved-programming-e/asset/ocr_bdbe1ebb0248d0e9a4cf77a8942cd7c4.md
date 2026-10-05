# C.7.5 Write a program that reads an integer and displays it in binary. Use an array to store the bits of the number. To display the bits of a negative number using the two's complement technique. For example, if the user enters -5:

+   a. convert it to positive (i.e., 5).
b. reverse its bits (i.e., 101, becomes 111111111111111111111111010),
c. add 1 (i.e., the number becomes 111111111111111111111111011, and that should be the output value).

```
#include <iostream>
using std::cout;
using std::cin;

int main()
{
    int i, j, tmp[32]; /* This array holds the bits of the number
    that is 0 or 1. The size is 32, because we assume that the size of an integer
    is 32. */
    unsigned int num;

    cout << "Number: ";
    cin >> tmp;
    if(tmp < 0)
    {
        tmp = -tmp;
        tmp = -tmp;
        tmp++;
    }
    num = tmp; // It is stored as positive.\n    i = 0;
    /* Successive divisions by 2 and store each bit in the respective
    array position. */
    while(num > 0)
    {
        bits[i] = num & 1;
        num >>= 1; // Equivalent to num /= 2;
        i++;
    }
    cout << "Binary form: ";
    // Display the bits from left to right.
    for(j=i-1; j>=0; j--)
        cout << bits[j];
    return 0;
}
```

Comments: The reason I used the shift operator is to improve performance. However, it is unnecessary most likely, because the compiler would optimize the operation by itself.

# C.7.6 What is the output of the following program?

```
#include <iostream>
int main()
{
    int i, a[] = {-1, 5, 7}, b[] = {5, 4, -1};
```