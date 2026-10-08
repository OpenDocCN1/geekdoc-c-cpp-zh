```
int raisetopower(int i_number, int i_power)
{
if(i_power == 0)
return (1);
else
return (i_number * raisetopower(i_number, i_power - 1));
}
/* End of function raisetopower */
/* Beginning of function main */
main()
{
/* Declare local variables */
int i_number, i_power, i_result;
/* Accept value from user */
printf("\nEnter the number: ");
scanf("%d", &i_number);
printf("\nEnter the power: ");
scanf("%d", &i_power);
/* Check if power is positive or not */
if(i_power > 0)
{
/* Call function raisetopower */
i_result = raisetopower(i_number, i_power);
printf("\nThe number %d raised to the power of %d is %d.\n",
i_number, i_power, i_result);
}
else
printf("\nCalculation for negative power is not performed.\n");
return;
}
/* End of function main */
```

# Output 1:

Enter the number: 3

Enter the power: 2

The number 3 raised to the power of 2 is 9.

# Output 2:

Enter the number: -5

Enter the power: 3

The number -5 raised to the power of 3 is -125.

# Output 3:

Enter the number: 9

Enter the power: -2

Calculation for negative power is not performed.