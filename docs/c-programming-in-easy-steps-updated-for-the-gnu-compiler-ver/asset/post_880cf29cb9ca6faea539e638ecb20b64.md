
## Looping for a number

A loop is a piece of code in a program that automatically repeats. One complete execution of all statements within a loop is called an “iteration”, or a “pass”. The length of a loop is controlled by a conditional test made within the loop. While the tested expression is found to be true, the loop will continue – until the tested expression is found to be false, at which point the loop ends.

In C programming there are three types of loop structure – for loops, while loops, and do while loops. Perhaps the most common of these is the for loop, which typically has this syntax:

```
for ( initializer ; test-expression ; incrementer ) { statements }
```

The initializer is used to set a starting value for a counter of the number of iterations made by the loop. An integer variable is used for this purpose and is traditionally named “i”.

Upon each iteration of the loop the test-expression is evaluated and that iteration will only continue while this expression is true. When the test-expression becomes false the loop ends immediately without executing the statements again. With every iteration the counter is incremented then the statements executed.

Loops can be nested, one within another, to allow complete execution of all iterations of an inner nested loop on each iteration of the outer loop.

![](img/d1dfb0563339ba187decb78799155b7f_77_0.png)

![](img/d1dfb0563339ba187decb78799155b7f_77_1.png)

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions
  
  ```c
  #include <stdio.h>
  ```

- 2. Add a main function that declares two integer variables to be used later as loop iteration counters
  
  ```c
  int main()
  {
      int i , j ;
  }
  ```

- 3. Next, in the main function block, insert a for loop to output the loop counter value on each of three iterations
  
  ```c
  for( i = 1 ; i < 4 ; i++ )
  {
      printf( "Outer loop iteration %d\n" , i ) ;
  }
  ```

- 4. At the end of the main function block, return a zero integer value, as required by the function declaration
  
  ```c
  return 0 ;
  ```

- 5. Save the program file, then compile and execute the program to see output from the for loop
  
  ```
  C:\MyPrograms>gcc forloop.c -o forloop.exe
  C:\MyPrograms>forloop
  Outer loop iteration 1
  Outer loop iteration 2
  Outer loop iteration 3
  C:\MyPrograms>
  ```

- 6. Now, in the loop block, insert a nested loop immediately after the existing output statement, to output the loop counter value on each of three inner loop iterations
  
  ```c
  for(j = 1 ; j < 4 ; j++)
  {
      printf( "\tInner loop iteration %d\n" , j ) ;
  }
  ```

- 7. Save the program file, then compile and execute the program once more to see output from both loops
  
  > **Hot Tip**
  >
  > A for loop counter can also count down – by decrementing the counter value on each iteration using `i--` instead of `i++`.
  
  ```
  C:\MyPrograms>gcc forloop.c -o forloop.exe
  C:\MyPrograms>forloop
  Outer loop iteration 1
    Inner loop iteration 1
    Inner loop iteration 2
    Inner loop iteration 3
  Outer loop iteration 2
    Inner loop iteration 1
    Inner loop iteration 2
    Inner loop iteration 3
  Outer loop iteration 3
    Inner loop iteration 1
    Inner loop iteration 2
    Inner loop iteration 3
  C:\MyPrograms>
  ```

## Looping while true

A while loop is an alternative to the for loop described in the previous example. The **while** loop also requires an initializer, test-expression, and incrementer, but these are not neatly listed within a single pair of parentheses as they are in a **for** loop. Instead, the initializer must appear before the start of the loop block, and the test-expression must appear within parentheses after the **while** keyword, followed by braces containing both an incrementer and the statements to be executed on each iteration.

```
initializer
while ( test-expression )
{ statements-to-be-executed ; incrementer }
```

![](img/d1dfb0563339ba187decb78799155b7f_79_0.png)

Notice that a semi-colon terminator is required after the while statement in the do while loop.

A do while loop provides a subtle variation on the syntax above by placing the do keyword before the loop block and moving the while statement to after the loop block.

```
initializer
do { statements-to-be-executed ; incrementer }
while ( test-expression ) ;
```

Both while loops and do while loops will proceed to make iterations until the test-expression is found to be false, at which point the loop will exit. It is therefore essential that the loop body contains code that will, at some point, change the result of the test-expression evaluation – otherwise an infinite loop is created that will lock the system.

The significant difference between a while loop and a do while loop is that a while loop will not make a single iteration if the test-expression is false on its first evaluation. In contrast, a do while loop will always make at least one iteration because its statements are executed before the evaluation is made. If this is desirable a do while loop is obviously the best choice, otherwise the choice between a for loop and a while loop is largely a matter of personal preference. One rule of thumb suggests that a for loop is best used to perform a specific number of iterations, whereas a while loop is best used to iterate until a certain condition is met.

![](img/d1dfb0563339ba187decb78799155b7f_79_1.png)

In the event that a program runs an infinite loop, on Windows or Linux systems press the Ctrl + C keyboard keys to halt the loop execution.

Loops are the perfect partner to use with arrays as each iteration can effortlessly read or write into successive array elements.

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions
  
  ```c
  #include <stdio.h>
  ```

![](img/d1dfb0563339ba187decb78799155b7f_80_0.png)

- 2. Add a main function that declares a counter variable then declares and initializes an array variable of three elements
  
  ```c
  int main()
  {
      int i , arr[3] = { 10 , 20 , 30 } ;
  }
  ```

- 3. Next, in the main function block, insert a while loop that outputs each element number and the value it contains
  
  ```c
  i = 0 ;
  while( i < 3 )
  {
      printf( "While: arr[%d] = %d\n" , i, arr[i] ) ;  i++ ;
  }
  ```

- 4. Now, insert a do while loop that also outputs each element number and the value it contains
  
  ```c
  i = 0 ;
  do
  {
      printf( "\nDo while: arr[%d] = %d" , i, arr[i] ) ; i++ ;
  }
  while( i < 3 ) ;
  ```

- 5. At the end of the main function block, return a zero integer value, as required by the function declaration
  
  ```c
  return 0 ;
  ```

> **Don't forget!**
>
> Change the value in this test-expression to zero — so `while (i<0)` in both loops — then recompile and run the program again to see only the first iteration of the **do while** loop get executed.

- 6. Save the program file, then compile and execute the program to see apparently identical output from the loops
  
  ```
  C:\MyPrograms>gcc dowhile.c -o dowhile.exe
  
  C:\MyPrograms>dowhile
  While: arr[0] = 10
  While: arr[1] = 20
  While: arr[2] = 30
  
  Do while: arr[0] = 10
  Do while: arr[1] = 20
  Do while: arr[2] = 30
  
  C:\MyPrograms>
  ```

## Breaking out of loops

The break keyword can be used to prematurely terminate a loop when a specified condition is met. The break statement is situated inside the loop statement block and is preceded by a test-expression. When the test returns true, the loop ends immediately and the program proceeds on to the next task. For example, in a nested inner loop it proceeds to the next iteration of the outer loop.

![](img/d1dfb0563339ba187decb78799155b7f_81_0.png)

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions
  
  ```c
  #include <stdio.h>
  ```

- 2. Add a main function that declares two integer variables to be used later as loop iteration counters
  
  ```c
  int main()
  {
      int i, j;
  }
  ```

- 3. Next, in the main function block, insert two nested loops to output their counter values on each of three iterations
  
  ```c
  for(i = 1; i < 4; i++)
  {
      for(j = 1; j < 4; j++)
      {
          printf("Running i=%d j=%d\n", i, j);
      }
  }
  ```

- 4. At the end of the main function block, return a zero integer value, as required by the function declaration
  
  ```c
  return 0;
  ```

- 5. Save the program file, then compile and execute the program to see the output from nested loops

![](img/d1dfb0563339ba187decb78799155b7f_81_1.png)
