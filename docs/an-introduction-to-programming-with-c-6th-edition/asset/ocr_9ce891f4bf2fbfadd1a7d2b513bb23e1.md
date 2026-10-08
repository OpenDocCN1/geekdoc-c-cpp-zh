# LAB 9-1 Stop and Analyze

Study the program in Figure 9-39, and then answer the questions.

The answers to the labs are located in Appendix A.

```
#include <iostream>
#include <ctime>
using namespace std;

int main() {
    // declare variables
    int randomNumber = 0;
    int numberGuess = 0;

    //generate a random number from 1 through 10
    srand(static_cast<int>(time(0)));
    randomNumber = 1 + rand() % (10 - 1);

    //get first number guess from user
    cout << "Guess a number from 10: ";
    cin >> numberGuess;
    while (numberGuess != randomNumber) {
        cout << "Sorry, guess again: ";
        cin >> numberGuess;
    }
    cout << endl << "Yes, the number is " << randomNumber << "." << endl;
    return 0;
}
```

> your C++ development tool may not require this statement

Figure 9-39 Code for Lab 9-1

# QUESTIONS

+   1. Why is the instruction on Line 5 necessary?
2. What is the purpose of the statement on Line 15?
3. If the rand function on Line 16 returns the number 453, what number will be assigned to the randomNumber variable?
4. Follow the instructions for starting C++ and opening Lab9-1.cpp file. The file is contained in the Cpp6[Chap09.Lab9-1 Project folder or the Cpp6[Chap09. found. Run the program from number 10. If you enter the correct number, the program displays "Yes, the number is x" message, in which x is the number