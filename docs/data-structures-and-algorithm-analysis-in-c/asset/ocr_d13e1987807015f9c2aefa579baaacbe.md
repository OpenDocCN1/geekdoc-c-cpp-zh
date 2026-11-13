```
1 /**
2  * Recursive maximum contiguous subsequence sum algorithm.
3  * Finds maximum sum in subarray spanning a[left..right].
4  * Does not attempt to maintain actual best sequence.
5  *
6  * int maxSubRec( const vector<int>& a, int left, int right )
7  {
8  if( left == right )  // Base case
9  {
10  if( a[ left ] > 0 )
11  return a[ left ];
12  else
13  return 0;
14 }
15
16 int center = ( left + right ) / 2;
17 int maxLeftSum  = maxSumRec( a, left, center );
18 int maxRightSum = maxSumRec( a, center + 1, right );
19
20 int maxLeftBorderSum = 0, leftBorderSum = 0;
21 for( int i = center; i >= left; --i )
22 {
23  leftBorderSum += a[ i ];
24  if( leftBorderSum > maxLeftBorderSum )
25  maxLeftBorderSum = leftBorderSum;
26 }
27
28 int maxRightBorderSum = 0, rightBorderSum = 0;
29 for( int j = center + 1; j <= right; ++j )
30 {
31  rightBorderSum += a[ j ];
32  if( rightBorderSum > maxRightBorderSum )
33  maxRightBorderSum = rightBorderSum;
34 }
35
36 return max3( maxLeftSum, maxRightSum,
37  maxLeftBorderSum + maxRightBorderSum );
38 }
39
40 /**
41  * Driver for divide-and-conquer maximum contiguous
42  * subsequence sum algorithm.
43  */
44 int maxSubSum3( const vector<int>& a )
45 {
46  return maxSumRec( a, 0, a.size( ) - 1 );
47 }
```

**Figure 2.7 Algorithm 3**