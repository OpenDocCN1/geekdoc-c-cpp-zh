To determine the sequence of operations needed in our function to make, we will work through a specific example. Suppose the amount of a purchase is $7.49 and we pay with a $10 bill. We clearly must begin by subtracting the purchase amount from the payment to get the amount of change. Also, at some point we must convert this real value to an integer value. One approach would be to store the total amount of change (2.51) as a real value and perform a separate conversion as each return value is computed. However, this requires doing the same thing six times—an indication that there is probably a better way. Also, real values are not stored exactly (e.g., 2.51 might be stored as 2.50993 ...) and thus it is better to round them to the nearest cent (2.51) and then convert this real amount into an integer value (251) at the outset, ensuring that no significant digits are lost. This can be done by multiplying the real amount of change by 100, adding 0.5, and then truncating the fractional part of the result. The following examples illustrate this computation:

![](bbox=[0.05, 0.3, 0.95, 0.42])

The result of this computation is the change in cents, and we will store this value in a local integer variable change.

Once change has been computed as the amount of change in cents, the number of dollars of change can be computed using integer division, dividing the value of change by 100:

```
dollars = change / 100; // for change = 251, dollars equals 2
```

The remaining change is the remainder that results from this division:

```
change %= 100; // for change = 251, change becomes 51
```

The number of quarters remaining in change can then be computed in a similar manner by dividing change by 25,

```
quarters = change / 25;
```

The remainder of this division is then the amount of change remaining to be dispensed as dimes, nickels, and pennies:

```
change %= 25;
```

Similar calculations are used to determine the number of dimes, nickels, and pennies. The complete function along with a driver program that tests it is shown in Example 10.3. The program reads two amounts (itemCost and amountPaid), calls makeChange() to calculate the change that must be given, and then displays the amounts passed back by makeChange().