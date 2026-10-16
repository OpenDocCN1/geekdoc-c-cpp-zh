
![](img/34f09be0ed6217c465debc4490197d4f_178_0.png)

## Figure 5.2

Each question is asked by a separate function, and information is passed between these functions and main().

// Yes or No
// Demonstrates return values and parameters

#include <iostream>
#include <string>

using namespace std;

char askYesNo1();
char askYesNo2(string question);

int main()
{
    char answer1 = askYesNo1();
    cout << "Thanks for answering: " << answer1 << "\n\n";

    char answer2 = askYesNo2("Do you wish to save your game?");
    cout << "Thanks for answering: " << answer2 << "\n";

    return 0;
}

```
char askYesNo1()
{
    char response1;
    do
    {
        cout << "Please enter 'y' or 'n': ";
        cin >> response1;
    } while (response1 != 'y' && response1 != 'n');

    return response1;
}
```

```
char askYesNo2(string question)
{
    char response2;
    do
    {
        cout << question << " (y/n): ";
        cin >> response2;
    } while (response2 != 'y' && response2 != 'n');

    return response2;
}
```

## Returning a Value

You can return a value from a function to send information back to the calling code. To return a value, you need to specify a return type and then return a value of that type from the function.

### Specifying a Return Type

The first function I declare, askYesNo1(), returns a char value. You can tell this from the function prototype before main():

```
char askYesNo1();
```

You can also see this from the function definition after main():

```
char askYesNo1(
```

## Using the return Statement

askYesNo1() asks the user to enter y or n and keeps asking until he does. Once the user enters a valid character, the function wraps up with the following line, which returns the value of response1.

```
return response1;
```

Notice that response1 is a char value. It has to be because that’s what I promised to return in both the function prototype and function definition.

A function ends whenever it hits a return statement. It’s perfectly acceptable for a function to have more than one return. This just means that the function has several points at which it can end.

### Trick

You don’t have to return a value with a return statement. You can use return by itself in a function that returns no value (one that indicates void as its return type) to end the function.

## Using a Returned Value

In main(), I call the function with the following line, which assigns the return value of the function to answer1.

```
char answer1 = askYesNo1();
```

This means that answer1 is assigned either 'y' or 'n'—whichever character the user entered when prompted by askYesNo1().

Next in main(), I display the value of answer1 for all to see.

## Accepting Values into Parameters

You can send a function values that it accepts into its parameters. This is the most common way to get information into a function.

### Specifying Parameters

The second function I declare, askYesNo2(), accepts a value into a parameter. Specifically, it accepts a value of type string. You can tell this from the function prototype before main():

```
char askYesNo2(string question);
```

### Hint

You don’t have to use parameter names in a prototype; all you have to include are the parameter types. For example, the following is a perfectly valid prototype that declares askYesNo2(), a function with one string parameter that returns a char.

```
char askYesNo2(string);
```

Even though you don’t have to use parameter names in prototypes, it’s a good idea to do so. It makes your code clearer, and it’s worth the minor effort.

From the header of askYesNo2(), you can see that the function accepts a string object as a parameter and names that parameter question.

```
char askYesNo2(string question)
```

Unlike prototypes, you must specify parameter names in a function definition. You use a parameter name inside a function to access the parameter value.

### Trap

The parameter types specified in a function prototype must match the parameter types listed in the function definition. If they don’t, you’ll generate a nasty compile error.

## Passing Values to Parameters

The askYesNo2() function is an improvement over askYesNo1(). The new function allows you to ask your own personalized question by passing a string prompt to the function. In main(), I call askYesNo2() with:

```
char answer2 = askYesNo2("Do you wish to save your game?");
```

This statement calls askYesNo2() and passes the string literal argument "Do you wish to save your game?" to the function.

## Using Parameter Values

askYesNo2() accepts "Do you wish to save your game?" into its parameter question, which acts like any other variable in the function. In fact, I display question with:

```
cout << question << " (y/n): ";
```

### Hint

> Actually, there’s a little more going on behind the scenes here. When the string literal "Do you wish to save your game?" is passed to question, a string object equal to the string literal is created and the string object gets assigned to question.

Just like askYesNo1(), askYesNo2() continues to prompt the user until he enters y or n. Then the function returns that value and ends.

Back in main(), the returned char value is assigned to answer2, which I then display.

## Understanding Encapsulation

You might not see the need for return values when you are using your own functions. Why not just use the variables response1 and response2 back in the main()? Because you can’t; response1 and response2 don’t exist outside of the functions in which they were defined. In fact, no variable you create in a function, including its parameters, can be directly accessed outside its function. This is a good thing, and it is called encapsulation. Encapsulation helps keep independent code truly separate by hiding or encapsulating the details. That’s why you use parameters and return values—to communicate only the information that needs to be exchanged. Plus, you don’t have to keep track of variables you create within a function in the rest of your program. As your programs get large, this is a great benefit.

Encapsulation might sound a lot like abstraction. That’s because they’re closely related. Encapsulation is a principal of abstraction. Abstraction saves you from worrying about the details, while encapsulation hides the details from you. As an example, consider a television remote control with volume up and down buttons. When you use a TV remote to change the volume, you’re employing abstraction because you don’t need to know what happens inside the TV for it to work. Now suppose the TV remote has 10 volume levels. You can get to them all through the remote, but you can’t directly access them. That is, you can’t get a specific volume number directly. You can only press the up volume and down volume buttons to eventually get to the level you want. The actual volume number is encapsulated and not directly available to you.

## UNDERSTANDING SOFTWARE REUSE

You can reuse functions in other programs. For example, since asking the user a yes or no question is such a common thing to do in a game, you could create an `askYesNo()` function and use it in all of your future game programs. So writing good functions not only saves you time and energy in your current game project, but it can save you effort in future ones, too.

## Real World

It’s always a waste of time to reinvent the wheel, so *software reuse*—employing existing software and other elements in new projects—is a technique that game companies take to heart. The benefits of software reuse include:

- **Increased company productivity.** By reusing code and other elements that already exist, such as a graphics engine, game companies can get their projects done with less effort.
- **Improved software quality.** If a game company already has a tested piece of code, such as a networking module, then the company can reuse the code with the knowledge that it’s bug-free.
- **Improved software performance.** Once a game company has a high-performance piece of code, using it again not only saves the company the trouble of reinventing the wheel, it saves them from reinventing a less efficient one.

You can reuse code you’ve written by copying from one program and pasting it into another, but there is a better way. You can divide up a big game project into multiple files. You’ll learn about this technique in Chapter 10, “Inheritance and Polymorphism: Blackjack.”

## WORKING WITH SCOPES

A variable’s *scope* determines where the variable can be seen in your program. Scopes allow you to limit the accessibility of variables and are the key to encapsulation, helping keep separate parts of your program, such as functions, apart from each other.

## Introducing the Scoping Program

The Scoping program demonstrates scopes. The program creates three variables with the same name in three separate scopes. The program displays the values of
