# Modify 4.3

4. If there are two times with the same maximum height, this program will print the first time that the maximum height occurred. Modify the program so that it will print the last time that the maximum height occurred.

# 4.7 Building C++ Solutions with IDEs: Microsoft Visual C++

In this section, we develop a C++ solution using Microsoft Visual C++ to illustrate the use of nested control structures. Our program implements the divide-and-conquer algorithm to guess a number between 1 and 20. The divide-and-conquer algorithm divides the range of possible guesses by two at each iteration by adjusting either the high or low value that defines the range. The guess is always the midpoint of the range.

Our program terminates when the number is guessed or the high value in the range becomes less than the low value. The second case will happen if the user does not answer each question correctly. The pseudocode for our number-guessing algorithm is given below:

```
Pseudocode
main: print greeting to user
while ((done && high > low)
   guess = (high + low)/2
   print guess
   if guess equals number
      print number of trys required to guess number
      done = true
   else if guess is larger than number
      increment number of tries
      high = guess - 1
   else if guess is smaller than number
      increment number of tries
      low = guess + 1
end while
```

The steps in the pseudocode are detailed enough to convert into C++. We use the ceil() function and the natural log function, log(), to predict how many tries it should take to guess the number, using our divide-and-conquer algorithm.

```
/***********************************************************/
/* Program chapter4_9                                      */
/* This program guesses a number between 1 and 20 inclusive. */
/***********************************************************/
#include<iostream>    //Required for cout, cin
#include<cmath>       //Required for cell, log
using namespace std;
int main()
{
```