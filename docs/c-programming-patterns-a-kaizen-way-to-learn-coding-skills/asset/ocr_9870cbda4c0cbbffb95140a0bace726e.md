```
printf("\n Accessing float array element using float pointer.\n");

// assigns the starting address of float array to the float pointer.
floatPtr = weight;

// finding size of array using C language's sizeof() operator.
size = sizeof( weight )/ sizeof( float );

for( int index = 0 ; index < size ; index++){

// using asterisk(*) indirection operator to print the array's element.
// total 5 digits to print float number and 2 digits after decimal point.

    printf( "%5.2f | ", *floatPtr);
    floatPtr ++ ;
}

printf("\n Accessing long array element using long pointer.\n");

// assigns the starting address of long array to the long pointer.
longPtr = distance;

// finding size of array using C language's sizeof() operator.
size = sizeof( distance )/ sizeof( long );

for( int index = 0 ; index < size ; index++){

// using asterisk(*) indirection operator to print the array's element.
// print long digit number.
    printf( "%ld | ", *longPtr);
    longPtr ++ ;
}
return 0;
```

# Output

Accessing char array element using char pointer.
M | r | . | A | l | w | a | y | s |  | R | i | g | h | t |

Accessing int array element using int pointer.
10 | 20 | 30 | 40 | 50 |

Accessing float array element using float pointer.
23.27 | 32.14 | 37.45 | 60.74 | 47.25 |

Accessing long array element using long pointer.
1234567 | 4335454 | 98767567 | 4354321 | 55558889 |