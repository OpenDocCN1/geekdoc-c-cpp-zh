Figure 13.2 If shown in full, the table would contain 10,000 rows and 32,768 individual numbers. The values in each row are equivalent modulus 10,000. All the columns except the rightmost column contain 10,000 entries.

![](bbox=[0.15, 0.21, 0.8, 0.53])

The first line verifies that the largest pseudorandom number that Visual C++ can produce through rand is 32,767. The next 10 lines that the program show the result of each trial, monitoring the activity of the one billion number generations. Since we are dealing with pseudorandom numbers, the results for each trial will not be exactly the same, but over one billion runs they should be close. Note how consistent the results are among the runs.

While we expected both 5 and 9,995 to appear about the same number of times—each approximately 100,000 times—in fact the number 5 appeared consistently more that 100,000 times, averaging 122,072 times. The number 9,995 appeared consistently less than 100,000 times, averaging 91,554.2. Note that 122,072 = 1.33; this means the value 5 appeared 1.33 times more often than 9,995. Looking at it another way, 133 ≈ 4/3, so for every four times the program produced a 5 it produced 9,995 only three times. As we soon will see, this ratio of 4:3 is not accidental.

Figure 13.2 shows why the expression rand( ) % 10000 does not produce an even distribution.

Figure 13.2 shows an abbreviated list of all the numbers the rand function can produce before applying the modulus operation. If you add the missing rows that the ellipses represent, the table would contain 10,000 rows. All of the four values in each row are equivalent modulus 10,000; thus, for example,

```
2 = 10,002 = 20,002 = 30,002
```