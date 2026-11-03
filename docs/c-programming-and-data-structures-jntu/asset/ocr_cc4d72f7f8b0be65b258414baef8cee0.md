```
printf("\nFINAL VALUE OF N IS NOT SUFFICIENT\n");
printf("TO ACHIEVE DESIRED ACCURACY\n");
goto end;
output:
printf("\nEXIT FROM LOOP\n");
printf("Sum = %f; No. of terms = %d\n", sum, n);
end:
;
}
Output
Input value of x : 21
EXIT FROM LOOP
Sum = 1.265800; No. of terms = 7
Input value of x : 75
EXIT FROM LOOP
Sum = 3.999774; No. of terms = 34
Input value of x : 99
FINAL VALUE OF N IS NOT SUFFICIENT
TO ACHIEVE DESIRED ACCURACY
```

# Fig. 7.9 Use of goto to exit from a loop

The test of accuracy is made using an if statement and the goto statement exits the loop as soon as the accuracy condition is satisfied. If the number of loop repetitions is not large enough to produce the desired accuracy, the program prints an appropriate message.

Note that the break statement is not very convenient to use here. Both the normal exit and the break exit will transfer the control to the same statement that appears next to the loop. But, in the present problem, the normal exit prints the message "FINAL VALUE OF N IS NOT SUFFICIENT TO ACHIEVE DESIRED ACCURACY" and the forced exit prints the results of evaluation. Notice the use of a null statement at the end. This is necessary because a program should not end with a label.

# Skipping a Part of a Loop—The Continue Statement

During the loop operations, it may be necessary to skip a part of the body of the loop under certain conditions. For example, in processing of applications for some job, we might like to exclude the processing of data of applicants belonging to a certain category. On reading the category code of an applicant, a test is made to see whether his application should be considered or not. If it is not to be considered, the part of the program loop that processes the application details is skipped and the execution continues with the next loop operation.

Like the break statement, C supports another similar statement called the continue statement. However, unlike the break which causes the loop to be terminated, the continue, as the name implies, causes the loop to be continued with the next iteration after skipping any statements in between. The continue statement tells the compiler, "SKIP THE FOLLOWING STATEMENTS AND CONTINUE WITH THE NEXT ITERATION". The format of the continue statement is simply