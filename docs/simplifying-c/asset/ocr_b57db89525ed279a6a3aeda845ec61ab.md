```
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
i_ocr = 1;

while(i_ocr<=i_row)
{
/* Beginning of action block of outer while loop */
i_ictr = 1;
while(i_ictr <= i_ocr)
{
/* Beginning of action block of inner while loop */
printf("$");
i_ictr++;
/* End of action block of inner while loop */
}

printf("\n");
i_ocr++;
/* End of action block of outer while loop */
}
return;
}
/* End of main function */
```

# **Output 1:**

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

Observe the use of do...while loop in Program 10. It has been used to validate the data, such that the value of row accepted by the program will always be a positive value greater