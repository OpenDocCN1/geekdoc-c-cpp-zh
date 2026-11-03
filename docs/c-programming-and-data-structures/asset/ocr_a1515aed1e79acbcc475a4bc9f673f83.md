```
Output:
average = sum/count;
range = high - low;
printf("\nTotal values : %d\n", count);
printf("Highest-value: %f\nLowest-value : %f\n", high, low);
printf("Range : %f\nAverage : %f\n", range, average);
}
```

Output
Enter numbers in a line : input a NEGATIVE number to end
35 40.50 25 31.25 68.15 47 26.65 29 53.45 62.50 -1
Total values : 10
Highest-value : 68.150002
Lowest-value : 25.000000
Range : 43.150002
Average : 41.849998

Fig. 2.14 Calculation of range of values

When the value is read the first time, it is assigned to two buckets, high and low, through the statement

```
high = low = value;
```

For subsequent values, the value read is compared with high; if it is larger, the value is assigned to high. Otherwise, the value is compared with low; if it is smaller, the value is assigned to low. Note that at a given point, the buckets high and low hold the highest and the lowest values read so far.

The values are read in an input loop created by the goto input; statement. The control is transferred out of the loop by inputting a negative number. This is caused by the statement

```
if (value < 0) goto output;
```

> NOTE: This program can be written without using goto statements. Try.

# 2. Pay-Bill Calculations

Problem: A manufacturing company has classified its executives into four levels for the benefit of certain perks. The levels and corresponding perks are shown below:

| Level | Perks | |
| | Conveyance allowance | Entertainment allowance |
| 1 | 1000 | 500 |
| 2 | 750 | 200 |
| 3 | 500 | 100 |
| 4 | 250 | – |

An executive’s gross salary includes basic pay, house rent allowance at 25% of basic pay and other perks. Income tax is withheld from the salary on a percentage basis as follows: