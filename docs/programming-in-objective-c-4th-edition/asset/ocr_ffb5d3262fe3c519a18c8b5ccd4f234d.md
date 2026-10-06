```
NSLog ("@ n Sum from 1 to n");
NSLog ("@-- ------");

triangularNumber = 0;

for ( n = 1; n <= 10; ++n ) {
    triangularNumber += n;
    NSLog ("@ %i, n%i", n, triangularNumber);
}

return 0;

```

# Program 5.3. Output

TABLE OF TRIANGULAR NUMBERS
n Sum from 1 to n
-- ----------
1 1
2 3
3 6
4 10
5 15
6 21
7 28
8 36
9 45
10 55

In Program 5.3, the purpose of the first three NSLog statements is simply to provide a general heading and to label the columns of the