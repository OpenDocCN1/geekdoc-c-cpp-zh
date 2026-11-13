```
// merge sorted SA0 suffixes and sorted SA12 suffixes
void merge( const vector<int>& s, const vector<int>& s12,
             vector<int>& sA, const vector<int>& sA0, const vector<int>& sA12,
             int n, int n0, int n12, int t )
{
   int p = 0, k = 0;

   while( t != n12 && p != n0 )
   {
      int i = getIndexIntoS( sA12, t, n0 ); // S12
      int j = sA0[ p ]; // S0

      if( suffix12IsSmaller( s, s12, sA12, n0, i, j, t ) )
      {
         sA[ k++ ] = i;
         ++t;
      }
      else
      {
         sA[ k++ ] = j;
         ++p;
      }
   }

   while( p < n0 )
      sA[ k++ ] = sA0[ p++ ];
   while( t < n12 )
      sA[ k++ ] = getIndexIntoS( sA12, t++, n0 );
}
```

# Figure 12.37 Merge the suffix arrays SA0 and SA12

Unlike binary search trees, for which clever O(logN) worst-case variants exist, there are no schemes that are known to guarantee a balanced 2-d tree. The problem is that such a scheme would likely be based on tree rotations, and tree rotations don't work in 2-d trees. The best one can do is to periodically rebalance the tree by reconstructing a subtree, as described in the exercises. Similarly, there are no deletion algorithms beyond the obvious lazy deletion strategy. If all the items arrive before we need to process queries, then we can construct a perfectly balanced 2-d tree in O(N log N) time; we leave this as Exercise 12.15(c).

Several kinds of queries are possible on a 2-d tree. We can ask for an exact match or a match based on one of the two keys; the latter type of request is a partial match query. Both of these are special cases of an (orthogonal) range query.

An orthogonal range query gives all items whose first key is between a specified set of values and whose second key is between another specified set of values. This is exactly the problem that was described in the introduction to this section. A range query is easily