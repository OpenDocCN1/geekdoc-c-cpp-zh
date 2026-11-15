The steps in the pseudocode are detailed enough to convert into C++. We use the ceil() function and the natural log function, log(), to predict how many tries it should take to guess the number, using our divide-and-conquer algorithm.

```
/*******************************************************************/
/* Program chapter4_9                                          */
/* This program guesses a number between 1 and 20 inclusive.      */
#include<iostream> //Required for cout, cin
#include<cmath>    //Required for ceil, log
using namespace std;

int main()
{
   // Declare and initialize objects
   int high(20), low(1), guess, count(1), ceiling;
   bool done(false);
   char answer;
   const char YES('Y'), NO('N');

   // Print greeting to user
   ceiling = ( ceil(log( double)high ) ) + 1 );
   cout << "Think of a number between " << low << "and " << high
        << " and I will guess it in" << ceiling
        << " or fewer tries. Just answer y(es) or n(o) to my questions.\n"
        << "Are you thinking of a number? " << endl;
   cin >> answer;
   switch(toupper(answer))
   {
   case YES:
      // While number has not been guessed
      while(!done && high >= low)
      {
         guess = (high + low)/2;
         cout << " Are you thinking of " << guess << "? " << endl;
         cin >> answer;
         switch(toupper(answer))
         {
         case YES:
            cout << " I guessed it in " << count << "tries." << endl;
            if(count > ceiling) cout << " Good pick.." << endl;
            done = true;
            break;
         case NO:
            //Must guess again.
            ++count;
            cout << " Is " << guess << " larger?" << endl;
            cin >> answer;
         }
      }
   }
}
```