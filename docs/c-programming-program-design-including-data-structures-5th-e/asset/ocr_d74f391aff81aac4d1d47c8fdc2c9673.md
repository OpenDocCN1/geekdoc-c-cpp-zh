```
```cpp
srand(time(0));
num = rand() % 100;
```
```

The first statement sets the seed, and the second statement generates a random number greater than or equal to 0 and less than 100. Note how the function time is used. It is used with an argument, that is, parameter, which is 0.

The program uses the bool variable isGuessed to control the loop. The bool variable isGuessed is initialized to false. It is set to true when the user guesses the correct number.

```
```cpp
//Flag-controlled while loop.
//Number guessing game.

#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

int main()
{
        //declare the variables
        int num;                          //variable to store the random
                                          //number
        int guess;                        //variable to store the number
                                          //guessed by the user
        bool isGuessed;                   //boolean variable to control
                                          //the loop

        srand(time(0));                   //Line 1
        num = rand() % 100;               //Line 2

        isGuessed = false;                //Line 3

        while (!isGuessed)                //Line 4
        {                                  //Line 5
                cout << "Enter an integer greater"
                     << " than or equal to 0 and"
                     << " less than 100: ";            //Line 6

                cin >> guess;             //Line 7
                cout << endl;             //Line 8

                if (guess == num)         //Line 9
                {                          //Line 10
                        cout << "You guessed the correct "
                             << "number." << endl;       //Line 11
                        isGuessed = true;                //Line 12
                }                          //Line 13
                else if (guess < num)      //Line 14
                        cout << "Your guess is lower than the "
                             << "number.\\n Guess again!"
                             << endl;                       //Line 15
```
```