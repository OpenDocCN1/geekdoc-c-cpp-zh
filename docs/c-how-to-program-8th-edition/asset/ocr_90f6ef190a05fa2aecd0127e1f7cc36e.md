```
```cpp
22    face = 1 + rand() % 6; // random number from 1 to 6
23
24    // determine roll value 1-6 and increment appropriate counter
25    switch ( face )
26    {
27        case 1:
28            ++frequency1; // increment the 1s counter
29            break;
30        case 2:
31            ++frequency2; // increment the 2s counter
32            break;
33        case 3:
34            ++frequency3; // increment the 3s counter
35            break;
36        case 4:
37            ++frequency4; // increment the 4s counter
38            break;
39        case 5:
40            ++frequency5; // increment the 5s counter
41            break;
42        case 6:
43            ++frequency6; // increment the 6s counter
44            break;
45        default: // invalid value
46            cout << "Program should never get here!";
47    } // end switch
48} // end for

50 cout << "Face" << setw( 13 ) << "Frequency" << endl; // output headers
51 cout << "\n    1" << setw( 13 ) << frequency1
52      << "\n    2" << setw( 13 ) << frequency2
53      << "\n    3" << setw( 13 ) << frequency3
54      << "\n    4" << setw( 13 ) << frequency4
55      << "\n    5" << setw( 13 ) << frequency5
56      << "\n    6" << setw( 13 ) << frequency6 << endl;
57} // end main
```
```

| Face | Frequency |
|---:|---:|
| 1 | 999702 |
| 2 | 1000823 |
| 3 | 999378 |
| 4 | 998898 |
| 5 | 1000777 |
| 6 | 1000422 |

# Fig. 6.9 | Rolling a six-sided die 6,000,000 times. (Part 2 of 2.)

As the output shows, we can simulate the rolling of a six-sided die by scaling and shifting the values produced by rand. The program should never get to the default case (lines 45–46) in the switch structure, because the switch’s controlling expression (face) always has values in the range 1–6; however, we provide the default case as a matter of good practice. After we study arrays in Chapter 7, we show how to replace the entire switch structure in Fig. 6.9 elegantly with a single-line statement.