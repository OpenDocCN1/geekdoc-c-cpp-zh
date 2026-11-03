# CHAPTER 5

# FLOW CONTROL - The while and for statements

The computer programming would not be very useful if, even with the condition assessment instructions, the execution could not go back and resume formulas already used to assign them new values a number of times. Imagine the embarrassment that it would be the simple printing of numbers from zero up to a thousand. With commands that allow the use of iterated variables, this is no problem.

# The while loop

Printing the numbers from zero to a thousand is easier than taking candy from a baby:

```
main(){int k=0;while(k<=1000){printf("%d ",k);k+=2;}}
```

Stating how integer the variable k; and initializing it to zero, the mini-program above tells the processor that while k is lesser than or equal to a thousand it should print k, then add 2 to the printed value and return to the word while. The instruction "k + 2;" uses the "+=" symbol, exclusive of C, and it would be written in Pascal as "k: = k+2," meaning that the value of k should be assigned the old variable value plus 2. If you want to run example above, be sure to add at the beginning the line #include <stdio.h>.

# The do-while loop

Another version of the while statement is given with the do-while couple, the use of which in some cases is more convenient. The difference is that the evaluation condition is made at the end of the loop. The same mini-program above would look like this:

```
main()
```