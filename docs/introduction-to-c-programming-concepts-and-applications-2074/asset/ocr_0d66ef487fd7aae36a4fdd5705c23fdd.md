# 12 Creating Your Own Functions in C++

+   IN THIS LECTURE:
- Functions as Black Boxes
- Creating Your Own Functions
- The Function Body
- Program 12_1
- Conceptual Separation
- Program 12_6
- Program 12_7
- Program 12_8
- Scope
- Program 12_ERROR_1
- Program 12_ERROR_2
- Program 12_10
- Program 12_11
- Program 12_12
- Quiz
- Quiz Answers

Functions are a key part of programming. They enable you to organize your programs by breaking up ideas into individual pieces—the functions—and they can sometimes save a lot of repeated coding. You've already been using functions; you've imported functions from libraries and used functions to get input, for file operations, and with vectors. All of these functions performed some computation for you, all by just making a function call.

# // FUNCTIONS AS BLACK BOXES

The easiest to think of a function as a so-called black box. You have some program, consisting of various instructions. When you want something to happen, you make a function call. You possibly send from the function input parameters; these are the arguments, then the function takes action, and possibly returns a final return value sent back to part of the program that called the function. But the inner workings of the function—that is, knowing what the function does—are hidden from the main program.

On the other hand, when you write a function, you don't have to worry about how it is used. You might be getting some input parameters, and you might know you need to return some particular value. But you shouldn't need to worry about it at all how that function is called. You don't care about the function's role in the main program; you need to know that the function is going to do its job.

This brings you the 2 main reasons why you have functions:

+   Functions offer a conceptual separation of ideas. Functions let you write code without worrying about details. Either you're writing a function and not worrying about how it is called or you're writing the calling program and not worrying about how the function works.

+   Using functions lets you avoid the work of writing the same code over and again.