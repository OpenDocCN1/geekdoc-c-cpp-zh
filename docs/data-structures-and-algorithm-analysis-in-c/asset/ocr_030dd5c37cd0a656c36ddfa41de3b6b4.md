```
1 // Compute the suffix array for s12, placing result into SA12
2 void computeS12( vector<int>& s12, vector<int>& SA12,
3                  int n12, int K12 )
4 {
5     if( K12 == -n12 ) // if unique names, don't need recursion
6         for( int i = 0; i < n12; ++i )
7             SA12[ s12[ i ] - 1 ] = i;
8     else
9     {
10        makeSuffixArray( s12, SA12, n12, K12 );
11        // store unique names in s12 using the suffix array
12        for( int i = 0; i < n12; ++i )
13            s12[ SA12[ i ] ] = i + 1;
14    }
15 }
16 
17 void computeS0( const vector<int>& s, vector<int>& s0,
18                 vector<int>& SA0, const vector<int>& SA12,
19                 int n0, int n12, int K )
20 {
21    for( int i = 0, j = 0; i < n12; ++i )
22        if( SA12[ i ] < n0 )
23            s0[ j++ ] = 3 * SA12[ i ];
24    radixPass( s0, SA0, s, n0, K );
25 }
26 }
```

# Figure 12.36 Compute the suffix array for s12 (possibly recursively) and the suffix array for s0

of matches reported by the query. We would like to obtain a similar bound for two or more dimensions.

The two-dimensional search tree has the simple property that branching on odd levels is done with respect to the first key, and branching on even levels is done with respect to the second key. The root is arbitrarily chosen to be an odd level. Figure 12.39 shows a 2-d tree. Insertion into a 2-d tree is a trivial extension of insertion into a binary search tree. As we go down the tree, we need to maintain the current level. To keep our code simple, we assume that a basic item is an array of two elements. We then need to toggle the level between 0 and 1. Figure 12.40 shows the code to perform an insertion. We use recursion in this section; a nonrecursive implementation that would be used in practice is straightforward and left as Exercise 12.17. One difficulty is duplicates, particularly since several items can agree in one key. Our code allows duplicates, and always places them in right branches; clearly this can be a problem if there are too many duplicates.

A moment's thought will convince you that a randomly constructed 2-d tree has the same structural properties as a random binary search tree: The height is O(log N) on average, but O(N) in the worst case.