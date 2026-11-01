
## The tellStory() Function

The tellStory() function takes all of the information entered by the user and uses it to display a personalized story.

```
void tellStory(string name, string noun, int number, string bodyPart,
    string verb)
{
    cout << "\nHere's your story:\n";
    cout << "The famous explorer ";
    cout << name;
    cout << " had nearly given up a life-long quest to find\n";
    cout << "The Lost City of ";
    cout << noun;
    cout << " when one day, the ";
    cout << noun;
    cout << " found the explorer.\n";
    cout << "Surrounded by ";
    cout << number;
    cout << " " << noun;
    cout << ", a tear came to ";
    cout << name << "'s ";
    cout << bodyPart << ".\n";
    cout << "After all this time, the quest was finally over. ";
    cout << "And then, the ";
    cout << noun << "\n";
    cout << "promptly devoured ";
    cout << name << ".";
    cout << "The moral of the story? Be careful what you ";
    cout << verb;
    cout << " for.";
}
```

## SUMMARY

In this chapter, you should have learned the following concepts:

- Functions allow you to break up your programs into manageable chunks.
- One way to declare a function is to write a function prototype—code that lists the return value, name, and parameter types of a function.
- Defining a function means writing all the code that makes the function tick.
- You can use the `return` statement to return a value from a function. You can also use `return` to end a function that has `void` as its return type.
- A variable's scope determines where the variable can be seen in your program.
- Global variables are accessible from any part of your program. In general, you should try to limit your use of global variables.
- Global constants are accessible from any part of your program. Using global constants can make your program code clearer.
- Default arguments are assigned to a parameter if no value for the parameter is specified in the function call.
- Function overloading is the process of creating multiple definitions for the same function, each of which has a different set of parameters.
- Function inlining is the process of asking the compiler to inline a function—meaning that the compiler should make a copy of the function everywhere in the code where the function is called. Inlining very small functions can sometimes yield a performance boost.

## QUESTIONS AND ANSWERS

Q: Why should I write functions?

A: Functions allow you to break up your programs into logical pieces. These pieces result in smaller, more manageable chunks of code, which are easier to work with than a single monolithic program.

Q: What’s encapsulation?

A: At its core, encapsulation is about keeping things separate. Function encapsulation provides that variables declared in a function are not accessible outside the function, for example.

Q: What’s the difference between an argument and a parameter?

A: An argument is what you use in a function call to pass a value to a function. A parameter is what you use in a function definition to accept values passed to a function.

Q: Can I have more than one `return` statement in a function?

A: Sure. In fact, you might want multiple `return` statements to specify different end points of a function.

Q: What's a local variable?

A: A variable that's defined in a scope. All variables defined in a function are local variables; they're local to that function.

Q: What does it mean to hide a variable?

A: A variable is hidden when you declare it inside a new scope with the same name as a variable in an outer scope. As a result, you can't get to the variable in the outer scope by using its variable name in the inner scope.

Q: When does a variable go out of scope?

A: A variable goes out of scope when the scope in which it was created ends.

Q: What does it mean when a variable goes out of scope?

A: It means the variable ceases to exist.

Q: What's a nested scope?

A: A scope created within an existing scope.

Q: Must an argument have the same name as the parameter to which it's passed?

A: No. You're free to use different names. It's only the value that's passed from a function call to a function.

Q: Can I write one function that calls another?

A: Of course. In fact, whenever you write a function that you call from `main()`, you're doing just that. In addition, you can write a function (other than `main()`) that calls another function.

Q: What is code profiling?

A: It's the process of recording how much CPU time various parts of a program use.

Q: Why profile code?

A: To determine any bottlenecks in a program. Sometimes it makes sense to revisit these sections of code in an attempt to optimize them.

Q: When do programmers profile code?

A: Usually toward the end of the programming of a game project.

Q: What's premature optimization?

A: An attempt to optimize code too early in the development process. Code optimization usually makes sense near the end of programming a game project.

## DISCUSSION QUESTIONS

- 1. How does function encapsulation help you write better programs?
- 2. How can global variables make code confusing?
- 3. How can global constants make code clearer?
- 4. What are the pros and cons of optimizing code?
- 5. How can software reuse benefit the game industry?

## EXERCISES

- 1. What's wrong with the following prototype?

  ```c
  int askNumber(int low =1, int high);
  ```

- 2. Rewrite the Hangman game from Chapter 4 using functions. Include a function to get the player's guess and another function to determine whether the player's guess is in the secret word.
- 3. Using default arguments, write a function that asks the user for a number and returns that number. The function should accept a string prompt from the calling code. If the caller doesn't supply a string for the prompt, the function should use a generic prompt. Next, using function overloading, write a function that achieves the same results.

## REFERENCES: TIC-TAC-TOE

The concept of references is simple, but its implications are profound. In this chapter, you'll learn about references and how they can help you write more efficient game code. Specifically, you'll learn to:

- Create references
- Access and change referenced values
- Pass references to functions to alter argument values or for efficiency
- Return references from a function for efficiency or to alter values

### USING REFERENCES

A reference provides another name for a variable. Whatever you do to a reference is done to the variable to which it refers. You can think of a reference as a nickname for a variable—another name that the variable goes by. In the first program in this chapter, I'll show you how to create references. Then, in the next few programs, I'll show you why you'd want to use references and how they can improve your game programs.

### Introducing the Referencing Program

The Referencing program demonstrates references. The program declares and initializes a variable to hold a score and then creates a reference that refers to the variable. The program displays the score using the variable and the reference to show that they access the same single value. Next, the program shows that this single value can be altered through either the variable or the reference. Figure 6.1 illustrates the program.

![](img/c7e8651578bccd573227f684823b8754_209_0.png)

![](img/c7e8651578bccd573227f684823b8754_210_0.png)

Figure 6.1
The variable myScore and the reference mikesScore are both names for the single score value.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 6 folder; the filename is referencing.cpp.

```
// Referencing
// Demonstrates using references

#include <iostream>

using namespace std;

int main()
{
    int myScore = 1000;
    int& mikesScore = myScore;  //create a reference

    cout << "myScore is: " << myScore << "\n";
    cout << "mikesScore is: " << mikesScore << "\n\n";
```
