you use subscripts rather than constant values. Then you can use a loop to perform arithmetic on each element in the array. For example, you can use a while loop, as follows:

```
int sub = 0;
while(sub < 5)
{
    myScores[sub] += 3;
    ++sub;
}
```

You can also use a for loop, as follows:

```
for(int sub = 0; sub < 5; ++sub)
myScores[sub] += 3;
```

In both examples, the variable sub is declared and initialized to 0, then compared to 5. Because it is less 5, the loop executes, and myScores[0] increases by 3. The variable sub is incremented and becomes 1, which is still less than 5, so the loop executes again, myScores[1] increases by 3, and so on. If the array had 100 elements, individually increasing the array values by 3 would require 95 additional statements, but the only change required using either loop would be to change the limit for sub from 5 to 100.

New arrays users sometimes think there is a permanent connection between a variable used as a subscript and the array with which it is used, but that is not the case. For example, if you vary sub from 0 to 10 to fill an array, you do not need to use sub later when displaying the array elements—either the same variable or a different variable can be used as a subscript elsewhere in the program.

# Using the Length Property

When you work with arrays, you must ensure that the subscript you use remains in the range of 0 through less the array's length. If you declare an array with five elements and use a subscript that is negative or more than 4, you will receive the error message IndexOutOfRangeException when you run the program. (You will learn about IndexOutOfRangeException in the chapter "Exception Handling.") This message means the index, or subscript, does not hold a value that legally access an array element. For example, if you declare an array of five integers, you can display them as follows:

```
int[] myScores = {100, 75, 88, 100, 90};
for(int sub = 0; sub < 5; ++sub)
WriteLine("{0}", myScores[sub]);
```