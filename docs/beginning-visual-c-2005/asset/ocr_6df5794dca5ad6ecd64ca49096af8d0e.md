# Decisions and Loops

```
```cpp
// Ex3_06.cpp
// Multiple case actions
#include <iostream>
using std::cin;
using std::cout;
using std::endl;

int main()
{
    char letter = 0;
    cout << endl << "Enter a small letter: ";
    cin >> letter;
    switch(letter*(letter >= 'a' && letter <= 'z'))
    {
    case 'a':
    case 'e':
    case 'i':
    case 'o':
    case 'u': cout << endl << "You entered a vowel.";
    break;
    case 0: cout << endl << "That is not a small letter.";
    break;
    default: cout << endl << "You entered a consonant.";
    }
    cout << endl;
    return 0;
}
```
```

# How It Works

In this example, you have a more complex expression in the switch. If the character entered isn’t a low-ercase letter, the expression:

(letter >= 'a' && letter <= 'z')

results in the value false; otherwise it evaluates to true. Because letter is multiplied by this expression, the value of the logical expression is cast to an integer (0 if the logical expression is false and 1 if it is true. Thus the switch expression evaluates to 0 if a lowercase letter was not entered and to the value of letter if it was. The statements following the case label case 0 are executed whenever the character code stored in letter does not represent a lowercase letter.

If a lowercase letter was entered, the switch expression evaluates to the same value as letter so for all values corresponding to vowels, the output statement following the sequence of case labels that have case values that are vowels. The same statement executes for any vowel because when any of these case labels is chosen successive statements are executed until the break statement is reached. You can see that a single action can be taken for a number of different cases by writing each of the case labels one after the other before the statements to be executed. If a lowercase letter that is a consonant is entered as program input, the default case label statement is executed.