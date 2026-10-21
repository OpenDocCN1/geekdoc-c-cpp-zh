
![](img/2359b0c604600c58fba3539c738a356e_337_0.png)

Figure 6-5

Using this basic definition of the logic, you can now write the function:

```
// Function to evaluate an arithmetic expression
double expr(char* str)
{
    double value = 0.0;                // Store result here
    int index = 0;                     // Keeps track of current character position

    value = term(str, index);          // Get first term
    for(;;)                            // Indefinite loop, all exits inside
{
    switch(*(str + index++))        // Choose action based on current character
    {
        case '\0':                  // We're at the end of the string
            return value;           // so return what we have got

        case '+':                   // + found so add in the
            value += term(str, index);  // next term
            break;

        case '-':                   // - found so subtract
            value -= term(str, index);  // the next term
            break;

        default:                    // If we reach here the string
            cout << endl            // is junk
                << "Arrgh!*#!! There's an error"
                << endl;
            exit(1);
    }
}
```

## How the Function Functions

Considering this function is analyzing any arithmetic expression that you care to throw at it (as long as it uses our operator subset), it’s not a lot of code. You define a variable index of type int, which keeps track of the current position in the string where you are working, and you initialize it to 0, which corresponds to the index position of the first character in the string. You also define a variable value of type double in which you’ll accumulate the value of the expression that is passed to the function in the char array str.

Because an expression must have at least one term, the first action in the function is to get the value of the first term by calling the function term(), which you have yet to write. This actually places three requirements on the function term():

- 1. It should accept a char* pointer and an int variable as parameters, the second parameter being an index to the first character of the term in the string supplied.
- 2. It should update the index value passed to position it at the character following the last character of the term found.
- 3. It should return the value of the term as type double.

The rest of the program is an indefinite for loop. Within the loop, the action is determined by a switch statement, which is controlled by the current character in the string. If it is a '+', you call the term() function to get the value of the next term in the expression and add it to the variable value. If it is a '-', we subtract the value returned by term() from the variable value. If it is a '\0', you are at the end of the string, so you return the current contents of the variable value to the calling program. If it is any other character, it shouldn’t be there, so after remonstrating with the user you end the program!

As long as either a '+' or a '-' is found, the loop continues. Each call to term() moves the value of the index variable to the character following the term that was evaluated, and this should be should be either another '+' or '-', or the end of string character '\0'. Thus, the function either terminates

normally when '\0' is reached, or abnormally by calling exit(). You need to remember the #include directive for <cstdlib> header file that provides the definition of the function exit() when you come to put the whole program together.

You also could also analyze an arithmetic expression using a recursive function. If you think about the definition of an expression slightly differently, you could specify it as being either a term, or a term followed by an expression. The definition here is recursive (i.e. the definition involves the item being defined), and this approach is very common in defining programming language structures. This definition provides just as much flexibility as the first, but using it as the base concept, you could arrive at a recursive version of expr() instead of using a loop as you did in the implementation above. You might want to try this alternative approach as an exercise after you have completed the first version.

## Getting the Value of a Term

The term() function returns a value for a term as type double and receive two arguments: the string being analyzed and an index to the current position in the string. There are other ways of doing this, but this arrangement is quite straightforward. You can, therefore, write the prototype of the function term() as follows:

```
double term(char* str, int& index);      // Function analyzing a term
```

You have specified the second parameter as a reference. This is because you want the function to be able to modify the value of the variable index in the calling program to position it at the character following the last character of the term found in the input string. You could return index as a value, but then you would need to return the value of the term in some other way, so this arrangement seems quite natural.

The logic for analyzing a term is going to be similar in structure to that for an expression. A term is a number, potentially followed by one or more combinations of a multiply or a divide operator and another number. You can write the definition of the term() function as follows:

```
// Function to get the value of a term
double term(char* str, int& index)
{
    double value = 0.0;                  // Somewhere to accumulate
                                       // the result

    value = number(str, index);          // Get the first number in the term

    // Loop as long as we have a good operator
    while((*(str + index) == '*') || (*(str + index) == '/'))
    {
        if(*(str + index) == '*')         // If it's multiply,
            value *= number(str, ++index); // multiply by next number

        if(*(str + index) == '/')         // If it's divide,
            value /= number(str, ++index); // divide by next number
    }
    return value;                        // We've finished, so return what
                                         // we've got
}
```

## How the Function Functions

You first declare a local double variable, value, in which you’ll accumulate the value of the current term. Because a term must contain at least one number, the first action in the function is to obtain the value of the first number by calling the number() function and storing the result in value. You implicitly assume that the function number() accepts the string and an index to a position in the string as arguments, and returns the value of the number found. Because the number() function must also update the index to the string to the position after the number that was found, you’ll again specify the second parameter as a reference when you come to define that function.

The rest of the term() function is a while loop that continues as long as the next character is '*' or '/'. Within the loop, if the character found at the current position is '*', you increment the variable index to position it at the beginning of the next number, call the function number() to get the value of the next number, and then multiply the contents of value by the value returned. In a similar manner, if the current character is '/', you increment the index variable and divide the contents of value by the value returned from number(). Because the function number() automatically alters the value of the variable index to the character following the number found, index is already set to select the next available character in the string on the next iteration.

The loop terminates when a character other than a multiply or divide operator is found, whereupon the current value of the term accumulated in the variable value is returned to the calling program.

The last analytical function that you require is number(), which determines the numerical value of any number appearing in the string.

## Analyzing a Number

Based on the way you have used the number() function within the term() function, you need to declare it with this prototype:

```
double number(char* str, int& index);  // Function to recognize a number
```

The specification of the second parameter as a reference allows the function to update the argument in the calling program directly, which is what you require.

You can make use of a function provided in a standard C++ library here. The <cctype> header file provides definitions for a range of functions for testing single characters. These functions return values of type int where positive values corresponding to true and zero corresponds to false. Four of these functions are shown in the following table:

| Functions in the <cctype> Header for Testing Single Characters |  |
|---|---|
| int isalpha(int c) | Returns true if the argument is alphabetic, false otherwise. |
| int isupper(int c) | Returns true if the argument is an upper case letter, false otherwise. |
| int islower(int c) | Returns true if the argument is a lower case letter, false otherwise. |
| int isdigit(int c) | Returns true if the argument is a digit, false otherwise. |
