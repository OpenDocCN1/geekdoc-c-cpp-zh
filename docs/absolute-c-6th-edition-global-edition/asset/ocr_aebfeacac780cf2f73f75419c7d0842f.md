These individual variables that together make up the array are referred to in a variety of different ways. We will call them indexed variables, though they are also sometimes called subscripted variables or elements of the array. The number in square brackets is called an index or a subscript. In C++, indexes are numbered starting with 0, not starting with 1 or any other number except 0. The number of indexed variables in an array is called the declared size of the array, or sometimes simply the size of the array. When an array is declared, the size of the array is given in square brackets after the array name. The indexed variables are then numbered (also using square brackets), starting with 0 and ending with the integer that is one less than the size of the array.

In our example, the indexed variables were of type int, but an array can have indexed variables of any type. For example, to declare an array with indexed variables of type double, simply use the type name double instead of int in the declaration of the array. All the indexed variables for one array, however, are of the same type. This type is called the base type of the array. Thus, in our example of the array score, the base type is int.

You can declare arrays and regular variables together. For example, the following declares the two int variables next and max in addition to the array score:

```
int next, score[5], max;
```

An indexed variable such as score[3] can be used anyplace that an ordinary variable of type int can be used.

Do not confuse the two ways to use the square brackets, [], with an array name. When used in a declaration, such as

```
int score[5];
```

the number enclosed in the square brackets specifies how many indexed variables the array has. When used anywhere else, the number enclosed in the square brackets tells which indexed variable is meant. For example, score[0] through score[4] are indexed variables of the array previously declared.

The index inside the square brackets need not be given as an integer constant. You can use any expression in the square brackets as long as the expression evaluates to one of the integers ranging from 0 through the integer one less than the size of the array. For example, the following will set the value of score[3] equal to 99:

```
int n = 2;
score[n + 1] = 99;
```

Although they may look different, score[n + 1] and score[3] are the same indexed variable in the previous code, because n + 1 evaluates to 3.

The identity of an indexed variable, such as score[i], is determined by the value of its index, which in this instance is i. Thus, you can write programs that say things like "do such and such to the i-th indexed variable," where the value of i is computed by the program. For example, the program in Display 5.1 reads in scores and processes them in the way described at the start of this chapter.

indexed variable, subscripted variable, or element

index or subscript

declared size

base type

![](bbox=[0.05, 0.85, 0.12, 0.95])