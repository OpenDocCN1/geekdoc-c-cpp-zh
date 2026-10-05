# C.6.15 Write a program that reads an integer and displays the number of its digits and their sum. For example, if the user enters 1234, the program should display 4 and 10 (1+2+3+4=10).

```
#include <iostream>
int main() {
    int num, sum, dig;

    sum = dig = 0;
    std::cout << "Enter number: ";
    std::cin >> num;

    if(num == 0)
        dig = 1;
    else
    {
        if(num < 0)
            num = -num;

        while (num != 0) {
            sum += num % 10;
            num /= 10; // Remove the last digit.
        }
    }
    std::cout << dig << " digits and their sum is " << sum << '\
';
    return 0;
```

# C.6.16 Write a program that reads an integer in [0, 255] continuously and displays it in binary. For example, if the user enters 32, the program should display 00100000. The program should also display the word Hi a number of times equal to the input. If the user enters a number out of [0, 255], the program should display the total number of the displayed Hi, terminate. It should also display the smallest and largest input number, as well as the average of the input numbers with a value in [8, 50]. Use while loops only.

```
#include <iostream>
using std::cout;
using std::cin;

int main() {
    int i, num, times, cnt, min, max, sum;

    times = cnt = sum = 0;
    min = 256;
    max = -1;
    while(1) {
        cout << "\nEnter number: ";
        cin >> num;
        if(num < 0 || num > 255)
            break;
```