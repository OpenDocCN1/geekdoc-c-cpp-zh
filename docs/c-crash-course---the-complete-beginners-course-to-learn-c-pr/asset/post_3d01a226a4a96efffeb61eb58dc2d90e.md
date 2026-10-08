when you created your code. It's important to remember that users will find errors that you probably won't find when you navigate through your code. You want to account for any coding error possibilities including any logic errors, so make sure you trap any possible errors in your try catch.

The last statement we display is the finally statement. This statement tells the compiler what to do before it exists. It's your last chance to run any type of statement before the program ends. For instance, you might have a file open statement in your code. Before the statement or program ends, you need to close that file to avoid locking it from any other process through the operating system. You can use the finally statement to close the file before the program and the code ends to avoid any bugs in your code.

To take our code step further, let's take a close look at a real-world example in our code.

```csharp
public void division(int num1, int num2)
{
    try
    {
        result = num1 / num2;
    }
    catch (DivideByZeroException e)
    {
        Console.WriteLine("Exception caught: {0}", e);
    }
    finally
    {
        Console.WriteLine("Result: {0}", result);
    }
}
```

Take a look at the above code to get an idea of how the try catch statement works within an actual application.

We created a division function that divides two numbers. The function takes two parameters that are used in the calculation to divide two numbers. As you recall from your math classes, you cannot divide by zero. If you don't have any type of try catch statement in your code, your users could accidentally send a zero value as the denominator and cause an error in your code. When you do this and don't account for the error, your program crashes and your users become frustrated with its functionality. You can overcome this issue by using the try catch statement that's included in the C# language.

If the user passes a zero value for the denominator, the catch block of code catches it and deals with it in a friendly way. This is important for your users when the program has issues, even if it's because of their own input. The catch phrase stops the program from crashing in an unfriendly way, and it deals with the error in a way that you want to use in your program.

In this example, we display an error to the user with the information returned from the program’s operating system. The catch block displays to the user that there was an error found in the code and displays information to it. This error is also returned from the operating system. This code is good for debugging, but it might not be very good for a real-world application. However, it's up to you how you deal with your coding errors.

The last statement for your catch block is the finally section. Remember that this is the block of code you want to add in case you you need to finalize any errors and change the code to something that doesn’t cause even more additional bugs in your programs from shutting down properly.

In our finally block, we print out the result, whether it’s a valid result value or an error in our code.

That's all it takes to create error handling in your code. Just remember that you should create user-friendly errors to avoid confusion for your users. This chapter gave you an example, but you can use any style of error handling that fits your program and what you need for your own users.

# Lab Questions

- 1. What is the first block or statement used in error handling for C#?
- a. try
- b. catch
- c. finally
- d. error
  > Explanation: The try statement wraps your code for error handling to provide friendly error messages to your users.

- 2. What is the statement that runs after all of your error handling is processed?
- a. try
- b. catch
- c. finally
- d. error
  > Explanation: The finally block runs the final section of code until the program exits or continues..

# Final Words

This is the start of your journey as a C# programmer. You have just barely scratched the surface with this guide, as learning the syntax and conventions of a language is just the beginning. The most important part of programming is the logical aspect of it. Sure, you may know how to loop through an array of variables like a list of shopping items, but if someone asks you to process an image using your knowledge of programming, with the help of an API and some thing you can figure out how to invert the colors of an image, flip it, rotate it, scale it, etc.

The real programming comes in the logical portion of the mind. It's similar to learning any other language, like English for example. You may understand the grammar rules and the conventions, like adding periods to the end of sentences—but the true skill lies in being able to write clean and logically thought-out structured essays. The same concept applies to programming, where the person writing the code must know how to apply or his knowledge of the rules of the language (like C#) and use it to his or her advantage to come up with neat programs.

The knowledge and understanding of programming is truly great because it's the closest thing we have to have magical powers. You can literally create something from scratch out of an empty notepad and have it to do things you want to do. Whether that be a bot to analyse and predict the stock market or a video game, that choice is yours.

In this guide you have learned the fundamentals of C#. You haven't learned all the possible methods that can be used in the language, but that isn't the point. This guide was designed to set you on a journey toward discovering objects and methods that you need in order to help you.

# Table of Contents

| Chapter | Topic |
| :--- | :--- |
| Chapter 1 | Introduction |
| Chapter 2 | C# Language |
| Chapter 3 | Data Types |
| Chapter 4 | Operators |
| Chapter 5 | Loops and If Statements |
| Chapter 6 | Introduction to OOP |
| Chapter 7 | Classes |
| Chapter 8 | Structures and Enums |
| Chapter 9 | Inheritance |
| Chapter 10 | Arrays |
| Chapter 11 | Generics |
| Chapter 12 | File I/O |
| Chapter 13 | Multithreading |
| Chapter 14 | Polymorphism |
| Chapter 15 | Error Handling |