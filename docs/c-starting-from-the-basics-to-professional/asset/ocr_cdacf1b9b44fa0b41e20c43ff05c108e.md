So this states, if letter equals 'A', then do nothing. But what is worse is that the second line is always executed, unconditionally, even if letter is different from 'A'—precisely what the if statement intended to prevent. Therefore, take care to never put a semicolon directly after a conditional test because it essentially nullifies the test!

You could extend the code fragment to change the value of letter if it contains the value 'A'.

```
if (letter == 'A')
{
    std::cout << "The first capital, alphabetically speaking.\n";
    letter = 'a';
}

std::cout << "This statement always executes.\n";
```

All the statements in the block will be executed when the if condition is true. Without the braces, only the first statement would be the subject of the if, and the if statement assigning the value 'a' to letter would always be executed. Of course, each of the statements in the block is terminated by a semicolon. No semicolon is necessary, though, after the closing brace of the block. You can have as many statements as you like within the block; you can even have nested blocks. If and when letter has the value 'A', both statements within the block will be executed, so its value will be changed to 'a' after the same message as before is displayed. Neither of these statements executes if the condition is false. The statement following the block always executes.

If you cast true to an integer type, the result will be 1; casting false to an integer results in 0. Conversely, you can also convert numerical values to type bool. Zero converts to false, and any nonzero value converts to true. When you have a numerical value where a bool value is expected, the compiler will insert an implicit conversion to convert the numerical value to type bool. This is useful in decision-making code.

Let's try an if statement for real. This program will range check the value of an integer entered from the keyboard:

```
// Ex4_03.cpp
// Using an if statement
import <iostream>;

int main()
{
    std::cout << "Enter an integer between 50 and 100: ";

    int value {};
    std::cin >> value;

    if (value)
        std::cout << "You have entered a value that is different from zero." << std::endl;

    if (value < 50)
        std::cout << "The value is invalid - it is less than 50." << std::endl;
}
```