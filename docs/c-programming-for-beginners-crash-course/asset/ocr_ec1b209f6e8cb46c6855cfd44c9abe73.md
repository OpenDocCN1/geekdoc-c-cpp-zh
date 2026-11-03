# Chapter 5: The Variables in the C Programming Language

As I mentioned a bit before, a variable is going to be the container for different data type sin your code. The variable, or the container, will be able to hold a floating point character, an integer, or some other value. In this chapter, I am going to explain a bit more about the variables and how you can use them, and how they work, inside of your C language code.

So how do you distinguish between a variable and a value. A value can be almost anything inside of the code, such as an integer, a character, or something else that can be defined in the code. On the other hand, the variable is going to be the container that holds these data types together. Usually they have to have something that ties them together, but they don’t need to be identical. For example, you could have a variable that contains school supplies such as pencils, pens, paper, chalk, notebooks, and so on. These are similar in one way, and they make sense to go together, but they are not identical.

When you declare a variable in the C language, you will learn about the type of variable and the name of the variable. Let’s take a look at how you would declare an integer variable to start:

```
#include <stdio.h>

Int main()
{
    Int a;

    Printf("The value of a is %d\n",a);

    Return(0);
}
```