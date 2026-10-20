```
int face; // most recently rolled value

// tally counts for 6,000,000 rolls of a die
for ( int roll = 1; roll <= 6000000; roll++ )
{
    face = 1 + randomNumbers.nextInt( 6 ); // number from 1 to 6

    // determine roll value 1-6 and increment appropriate counter
    switch ( face )
    {
        case 1:
            ++frequency1; // increment the 1s counter
            break;
        case 2:
            ++frequency2; // increment the 2s counter
            break;
        case 3:
            ++frequency3; // increment the 3s counter
            break;
        case 4:
            ++frequency4; // increment the 4s counter
            break;
        case 5:
            ++frequency5; // increment the 5s counter
            break;
        case 6:
            ++frequency6; // increment the 6s counter
            break; // optional at end of switch
    } // end switch
} // end for

System.out.println( "Face\tFrequency" ); // output headers
System.out.printf( "1%t%d\n2%t%d\n3%t%d\n4%t%d\n5%t%d\n6%t%d\n",
    frequency1, frequency2, frequency3, frequency4,
    frequency5, frequency6 );
} // end main
} // end class RollDie
```

| Face | Frequency |
|------|-----------|
| 1 | 999501 |
| 2 | 1000412 |
| 3 | 998262 |
| 4 | 1000820 |
| 5 | 1002245 |
| 6 | 998760 |

| Face | Frequency |
|------|-----------|
| 1 | 999647 |
| 2 | 999557 |
| 3 | 999571 |
| 4 | 1000376 |
| 5 | 1000701 |
| 6 | 1000148 |

Fig. 6.7 | Roll a six-sided die 6,000,000 times. (Part 2 of 2.)