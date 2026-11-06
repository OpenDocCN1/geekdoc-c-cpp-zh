```
cout << days << " days " << hours << " hours " << endl;
cout << minutes << " minutes and " << seconds << " seconds";
return 0;
}
```

# Exercise 13.1-4 — Reversing a Number

Write a C++ program that prompts the user to enter a three-digit integer and then reverses it. For example, if the user enters the number 375, the number 573 should be displayed.

# Solution

To isolate the three digits of the given number, you can use either first or second approach. Afterward, the only difficulty in this exercise is to build the reversed number. Take the number 375, for example. The three digits, after isolation, are

```
digit1 = 3;
digit2 = 7;
digit3 = 5;
```

You can build the reversed number by simply calculating the sum of the products:

digit3 × 100 + digit2 × 10 + digit1 × 1

For a change, you can split the given number using the second approach. The C++ program will look like this.

```
project_13_1_4

#include <iostream>
using namespace std;
int main() {
  int digit1, digit2, digit3, number, r, reversed;

  cout << "Enter a three-digit integer: " << endl;
  cin >> number;

  digit3 = number % 10;        //This is the rightmost digit
  r = (int)(number / 10);

  digit2 = r % 10;             //This is the digit in the middle
  digit1 = (int)(r / 10);       //This is the leftmost digit

  reversed = digit3 * 100 + digit2 * 10 + digit1;
  cout << reversed;
  return 0;
}
```