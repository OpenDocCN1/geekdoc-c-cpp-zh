a is equal to 0
a is equal to 1
a is greater than 1

Not what you expected? This is another common bug in C code - forgetting the break statements in your cases can result in very unexpected behaviour. But this can also be useful, programmers will sometimes structure a switch statement with code that they want to execute in multiple different cases, and deliberately leave out the break statements.

![](bbox=[0.116, 0.335, 0.883, 0.693])

Don't forget the break statements at the end of each case in your switch statements!

# YOUR FAVOURITE LOOP...

All three types of loop in C - while do and for - can be used in pretty many situations where a loop is needed; choose whichever you like. Some people prefer to use one type of loop for everything, others pick and choose which looks tidiest for each circumstance. There are no wrong choices.