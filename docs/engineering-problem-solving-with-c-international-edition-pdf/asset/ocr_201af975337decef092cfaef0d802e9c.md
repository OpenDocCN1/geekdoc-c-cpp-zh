with the rand() function to generate a new integer between 0 and n - 1. Finally, the lower limit, a, is added to the new integer to give a value between a and b. All three steps can be combined in one expression on the return statement in the function:

```
/*--------------------------------------------------------------*/
/* This function generates a random integer                     */
/* between specified limits a and b (a<b).                      */
/*--------------------------------------------------------------*/
int rand_int(int a, int b)
{
    return rand()%(b-a+1) + a;
}
/*--------------------------------------------------------------*/
```

To illustrate the use of this function, the next program generates 10 random integers between user-specified limits. The user also enters the seed to initiate the sequence:

```
/*--------------------------------------------------------------*/
/* Program chapter6_6                                          */
/* This program generates and prints ten random                 */
/* integers between user-specified limits.                      */
/*--------------------------------------------------------------*/
#include <cstdlib>   //Required for srand(), rand().
#include <iostream>  //Required for cin, cout.
using namespace std;

// Function prototype.
int rand_int(int a, int b);

int main()
{   // Declare objects.
    unsigned int seed;
    int a, b;

    // Get seed value and interval limits.
    cout << "Enter a positive integer seed value: \n";
    cin >> seed;

    //Seed the random number generator.
    srand(seed);
    cout << "Enter integer limits a and b (a<b): \n";
    cin >> a >> b;

    // Generate and print ten random numbers.
    cout << "Random Numbers: \n";
    for (int k=1; k<=10; ++k)
        cout << rand_int(a,b) << "  ";
    cout << endl;
}
```