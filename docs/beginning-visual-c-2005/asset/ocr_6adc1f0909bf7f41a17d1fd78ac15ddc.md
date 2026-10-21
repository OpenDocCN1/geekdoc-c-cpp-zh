```
*(primes + count++) = trial;  // ...so save it in primes array
}while(count < MAX);

// Output primes 5 to a line
for(int i = 0; i < MAX; i++)
{
    if(i % 5 == 0)                // New line on 1st, and every 5th line
        cout << endl;
    cout << setw(10) << *(primes + i);
}
cout << endl;
return 0;
}
```

If you compile and execute this example, you should get the following output:

2       3       5       7       11
13      17      19      23      29
31      37      41      43      47
53      59      61      67      71
73      79      83      89      97
101     103     107     109     113
127     131     137     139     149
151     157     163     167     173
179     181     191     193     197
199     211     223     227     229
233     239     241     251     257
263     269     271     277     281
283     293     307     311     313
317     331     337     347     349
353     359     367     373     379
383     389     397     401     409
419     421     431     433     439
443     449     457     461     463
467     479     487     491     499
503     509     521     523     541

# How It Works

You have the usual #include statements for the <iostream> header file for input and output and for <iomanip> because you will use a stream manipulator to set the field width for output.

You use the constant MAX to define the number of primes that you want the program to produce. The primes array, which stores the results, has the first three primes already defined to start the process off. All the work is done in two loops: the outer do-while loop, which picks the next value to be checked and adds the value to the primes array if it is prime, and the inner for loop that actually checks the value to see whether it’s prime or not.

The algorithm in the for loop is very simple and is based on the fact that if a number is not a prime, it must be divisible by one of the primes found so far — all of which are less than the number in question because all numbers are either prime or a product of primes. In fact, only division by primes less than or