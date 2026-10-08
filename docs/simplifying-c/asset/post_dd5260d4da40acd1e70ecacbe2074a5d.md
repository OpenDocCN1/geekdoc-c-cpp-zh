
![](img/5d422ba7108ffdf64376be51eaf0c459_157_0.png)

▲ Figure 8: Example of the Nested For Loop

It can be observed in Figure 8 that there are two for loops. The outer for loop is controlled by counter `i_octr` and has a statement in the action block, which itself is a for loop. The inner for loop is controlled by counter `i_ictr`. The inner for loop will be executed for every instance of `i_octr`. Program 9 illustrates the use of nested for loop.

### Program 9

```c
/* Program to print table of 1 and 2 using the nested for loop */
#include <stdio.h>

/* Beginning of main function */
main()
{
   /* Declare variable */
   int i_octr, i_ictr;

   for(i_octr = 1; i_octr <= 2; i_octr++)
   {
      /* Beginning of action block of outer for loop */
      printf("Table of %d\n", i_octr);
      printf("-----------\n");
      for(i_ictr = 1; i_ictr <= 10; i_ictr++)
      {
         /* Beginning of action block of inner for loop */
         printf("%2d * %2d = %2d\n", i_octr, i_ictr,
                i_octr*i_ictr);
         /* End of action block of inner for loop */
      }
      printf("\n");
      /* End of action block of outer for loop */
   }

   return;
}
/* End of main function */
```

**Output:**

```text
Table of 1
-----------
 1 *  1 =  1
 1 *  2 =  2
 1 *  3 =  3
 1 *  4 =  4
 1 *  5 =  5
 1 *  6 =  6
 1 *  7 =  7
 1 *  8 =  8
 1 *  9 =  9
 1 * 10 = 10

Table of 2
-----------
 2 *  1 =  2
 2 *  2 =  4
 2 *  3 =  6
 2 *  4 =  8
 2 *  5 = 10
 2 *  6 = 12
 2 *  7 = 14
 2 *  8 = 16
 2 *  9 = 18
 2 * 10 = 20
```

It can be observed from the output of Program 9 that for each occurrence of `i_octr`, the inner for loop is repeated 10 times. This means that for `i_octr` = 1, the inner for loop is repeated 10 times, and for `i_octr` = 2 also, the inner for loop is repeated 10 times. Note that the execution of the inner for loop is always completed first, and only then, the control is transferred back to the outer for loop.

Let us take one more example to understand the concept of nested loops better. Program 10 illustrates the use of nested loops to print a pattern on the monitor:

### Program 10

```c
/* Program to print pattern using nested loops */
# include <stdio.h>
/* Beginning of main function */
main()
{
	/* Declare variables */
	int i_row, i_temp, i_octr, i_ictr;

	/* Input data */
	/* Beginning of do...while loop */
	do
	{
		printf("Enter number of rows : ");
		scanf("%d", &i_row);

		/* Validate data */
		if(i_row <= 1)
			printf("\nEnter positive value greater than 1\n");
	}
	while(i_row <= 1);
	/* End of do...while loop */
	i_temp = i_row;

	/* Print the top pattern */
	for(i_octr=1; i_octr<=i_row; i_octr++)
	{
		/* Beginning of action block of outer for loop */
		for(i_ictr=1; i_ictr<=i_temp; i_ictr++)
		{
			/* Beginning of action block of inner for loop */
			printf("$");
			/* End of action block of inner for loop */
		}
		printf("\n");
		i_temp--;
		/* End of action block of outer for loop */
	}

	/* Print the bottom pattern */
	i_octr = 1;

	while(i_octr<=i_row)
	{
		/* Beginning of action block of outer while loop */
		i_ictr = 1;
		while(i_ictr <= i_octr)
		{
			/* Beginning of action block of inner while loop */
			printf("$");
			i_ictr++;
			/* End of action block of inner while loop */
		}

		printf("\n");
		i_octr++;
		/* End of action block of outer while loop */
	}
	return;
}
/* End of main function */
```

**Output 1:**

Enter number of rows: 4
$$$$
$$$
$$
$
$
$$
$$$
$$$$

It can be observed in Program 10 that we have used two nested loops, namely, a nested for loop and a nested while loop. This indicates that all the loop structures available in C language can be nested as per the needs. We can also generate a nested loop by using two different loop structures. For example, if a for statement is used as one of the executable statements within the action block of while loop, we still generate a nested loop.

Observe the use of do...while loop in Program 10. It has been used to validate the data, such that the value of row accepted by the program will always be a positive value greater than or equal to 1. Try to execute the program by entering a negative value and observe the output.

The execution sequence within the action block of the loops is again sequential. At times we need to alter the execution sequence within loops too. The next section discusses about how to alter the execution sequence within loops.

## 7.4 Altering Execution Control Flow in Loops

To alter the execution sequence within loops, C language provides us with four jump statements, as shown in Figure 9:

![](img/5d422ba7108ffdf64376be51eaf0c459_160_0.png)

These jump statements are `break`, `continue`, `return`, and `goto`. Each of the jump statement is used to alter the execution sequence.

The `break` and `return` statements have been used in many programs discussed in this book. Both these statements are used to come out of the current scope. The scope may be a decision structure, a loop structure, or a program. Normally, `return` statement is used to come out of the scope with a returning value, and `break` statement is used with the `case` keyword within `switch` structure. It is recommended not to use these keywords in other constructs.

In this section, we will discuss the remaining two jump statements, namely, `goto` and `continue`.

### The Goto Statement

The `goto` statement is the preliminary execution sequence altering statement. It is used for conditional or unconditional alteration of the execution sequence. The syntax of using the `goto` statement is as follows:

```c
goto label;
```

In the preceding syntax, the term `label` refers to an identifier defined in a program. A label is a special identifier that has its own name space in the memory. This name space only exists for the function containing the label; hence, the label names can be reused in different functions. The label identifier is the only identifiers in C language that can be used before it is declared. Figure 10 illustrates a forward jump and a backward jump using the `goto` statement.

![](img/5d422ba7108ffdf64376be51eaf0c459_161_0.png)

▲ Figure 10: Forward and Backward Jumps Using the Goto Statement

It can be observed in Figure 10 that an unconditional `goto` statement jumps to the specified label directly. While in case of conditional jump, we jump only when a condition is satisfied. The jumps are defined as forward jump or backward jump. If the execution control flow moves to statements below the use of `goto` statement, the jump is known as a forward jump. If the execution control flow moves to statements above the use of `goto` statement, the jump is known as a backward jump. As it is not recommended to use the `goto` statements in structured programming, hence detailed discussion of this topic has not been included in this book.

Another statement that alters the flow of execution is the `continue` statement. The next subsection discusses about the use of `continue`.

### The Continue Statement

The `continue` statement in C language is used to skip certain statements of the loop. It skips the execution of the statements that are written below the `continue` statement. The execution control flow is then transferred from the point where the statement `continue` is used to test conditions in the `while` and `do...while` loops. In case of the `for` loop, the execution control flow is transferred to expression 3 (loop counter update statement) of the `for` loop. Figure 11 illustrates how the execution control flow is transferred when we use the `continue` statement:

![](img/5d422ba7108ffdf64376be51eaf0c459_162_0.png)

It can be observed in Figure 11 that the syntax of using the `continue` statement is similar to that of the `break` statement. We only write the keyword and terminate it with a semicolon.

Note that the use of `break`, `continue`, `return`, and `goto` statements in loops is not considered to be a good way of programming. In case these statements appear in the loops, we should try to rewrite the logic of the program such that the jump statements get removed from the program.

## Summary

In this chapter, we have learned about the concept of repetition. The loops are categorized as pretest loop and posttest loop. In pretest loop, the test condition is checked at the time of entering the loop, while in posttest loop, it is checked at the time of exit. The posttest loop will always be executed once, while the pretest loop may not be executed at all. Both the pretest loop and the posttest loop can be governed by a counter or an event. If the loop is governed by a counter, it is called counter-controlled loop; when it is governed by an event, it is called event-controlled loop. C language provides us three loop constructs, namely, `for`, `while`, and `do...while`. The `for` and `while` loop constructs are pretest loops. The `do...while` loop construct is a posttest loop. Finally, we learned about the concept of nested loop and how to alter the flow of control within the loops using `break`, `continue`, `return`, and `goto` statements.

## Review Questions

- Q1. What is the significance of repetition in C program?
- Q2. Differentiate between pretest loops and posttest loops.
- Q3. Differentiate between event-controlled loops and counter-controlled loops.
- Q4. Explain with example the significance of null statement.
- Q5. Differentiate between `do...while` loop and `while` loop.
