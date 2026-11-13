```
1 /**
2  * Function that implements the basic primality test.
3  * If witness does not return 1, n is definitely composite.
4  * Do this by computing a^i (mod n) and looking for
5  * non-trivial square roots of 1 along the way.
6  *
7  HugeInt witness( const HugeInt & a, const HugeInt & i, const HugeInt & n )
8  {
9   if( i == 0 )
10   return 1;
11
12  HugeInt x = witness( a, i / 2, n );
13  if( x == 0 ) // If n is recursively composite, stop
14   return 0;
15
16  // n is not prime if we find a non-trivial square root of 1
17  HugeInt y = ( x * x ) % n;
18  if( y == 1 && x != 1 && x != n - 1 )
19   return 0;
20
21  if( i % 2 == 1 )
22   y = ( a * y ) % n;
23
24  return y;
25 }
26
27 /**
28  * The number of witnesses queried in randomized primality test.
29  *
30  const int TRIALS = 5;
31
32 /**
33  * Randomized primality test.
34  * Adjust TRIALS to increase confidence level.
35  * n is the number to test.
36  * If return value is false, n is definitely not prime.
37  * If return value is true, n is probably prime.
38  *
39  bool isPrime( const HugeInt & n )
40  {
41   Random r;
42
43  for( int counter = 0; counter < TRIALS; ++counter )
44   if( witness( r.randomHugeInt( 2, n - 2 ), n - 1, n ) != 1 )
45   return false;
46
47  return true;
48 }
```

Figure 10.63 A probabilistic primality testing algorithm