# Chapter 4: Using Loops Inside of the C Language

Loops can be a helpful thing to add into your code in the C language. These allow you to create lists of things or even graphs and charts inside of your code. They are nice because with just a few lines of code, you could get a huge chart done, rather than trying to type out each and every line that you need along the way. For example, if you wanted to make a chart that went from 1 to 100, it wouldn’t be much fun to write it all out for each line, but with the right loop statement, you would just need a few lines to make this happen.

Loops are another way that you are able to do comparisons inside of your code in the C language and there are several options for looping that can really add some power to your code. The while loop the nested loop, and the do/while loop are the most common types of these that you are able to use, but I will also spend some time talking about the for keyword in this chapter.

# The While Loop

A loop is going to be a control program execution that is very repetitive. You will be able to specify the condition that makes that loop repeat, as well as a set of statements that you want to repeat in the code, and a way for the loop to stop. If you forget to add in the part about stopping the loop, the program is basically going to keep going on forever and freezing up the computer so make sure that this is added in.

Here is an example of a code that will use the while loop in order to have the code count from 1 to 10.

```
```c
#include <stdio.h>

Int main()
{
    Int x;
```
```