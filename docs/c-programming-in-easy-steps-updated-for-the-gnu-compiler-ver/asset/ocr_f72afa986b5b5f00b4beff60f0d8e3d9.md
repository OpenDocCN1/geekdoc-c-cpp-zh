+   4. At the end of the main function block, return a zero integer value, as required by the function declaration
+       `return 0 ;`

+   5. Save the program file, then compile and execute the program to see output from the for loop

```
~~~
C:\MyPrograms>gcc forloop.c -o forloop.exe
C:\MyPrograms>forloop
Outer loop iteration 1
Outer loop iteration 2
Outer loop iteration 3
C:\MyPrograms>
~~~
```

+   6. Now, in the loop block, insert a nested loop immediately after the existing output statement, to output the loop counter value on each of three inner loop iterations

```
~~~
for(j = 1 ; j < 4 ; j++)
{
    printf( "\tInner loop iteration %d\n" , j ) ;
}
~~~
```

+   7. Save the program file, then compile and execute the program once more to see output from both loops

> > **Hot Tip**
> >
> > A for loop counter can also count down – by decrementing the counter value on each iteration using `i--` instead of `i++`.

```
~~~
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
~~~
```