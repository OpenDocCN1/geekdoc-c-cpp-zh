# Introduction to Arrays

These individual variables make up the array are referred to a variety of different ways. We will call them indexed variables, though they are sometimes called subscribed variables or elements of the array. In square brackets in C++, indexes are never starting with 0, not starting with 1 or any other number 0. The number of indexed variables in an array is called the size of the array, or sometimes simply the size of the array. When an array is declared, the size of the array is given in square brackets after the array name. The indexed variables are then numbered (using square brackets), starting with 0 and ending with the integer that is less than the size of the array.

In our example, the indexed variables were of type int, but an array can have indexed variables of any type. For example, to declare an array with indexed variables double, simply use the type name instead of in the declaration of the array. All indexed variables for one array, however, are of the same type. The type is called the base type of the array. Thus, by our example of the array score, the type is int.

You can declare arrays and regular variables together. For example, the declare two int variables next and in addition to the array score:

```
int next, score[5]; max;
```

An indexed variable as score[3] can be used anywhere that an ordinary variable of type int can be used.

Do not confuse the two ways to use the square brackets, [], with an array name. When used in a declaration, as

```
int score[5];
```

the number enclosed in the square brackets specifies how many indexed variables the array has. When used anywhere, the number enclosed in the square brackets tells which indexed variable is meant. For example, score[0] through score[4] are indexed variables of the array previously declared.

The inside square brackets need not be given as an integer constant. You can use any expression in the square brackets as evaluates one of the integers from 0 through the one less than the size of the array. For example, the following will set the score[3] equal to 99:

```
int n = 2;
score[n + 1] = 99;
```

Although they may look different, score[n + 1] and score[3] are the same indexed variables in the previous code, because n + 1 evaluates to 3.

The identity of an indexed variable, as score[i], is determined by the value of its index, which in this is i. You can write programs that say things like "do so and such to the ith indexed variable," where the value of i is computed by the program. For example, the program in Display 5.1 results in scores and processes in the way described at the start of this chapter.

![](bbox=[0.07, 0.783, 0.135, 0.856])