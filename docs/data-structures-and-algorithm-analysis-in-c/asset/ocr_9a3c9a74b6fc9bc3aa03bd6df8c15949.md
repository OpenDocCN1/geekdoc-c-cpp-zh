```
/**
 * Backtracking algorithm to place the points x[left] ... x[right].
 * x[1]...x[left-1] and x[right+1]...x[n] already tentatively placed.
 * If place returns true, then x[left]...x[right] will have values.
 */
/* place place(vector<int>& x, DistSet d, int n, int left, int right )
{
    int dmax;
    bool found = false;

1   if ( d.isEmpty( ) )
2       return true;
3   dmax = d.findMax( );

    // Check if setting x[right] = dmax is feasible.
4   if ( | x[ j ] - dmax | ∈ d for all 1 ≤ j < left and right < j ≤ n )
5   {
6       x[ right ] = dmax;        // Try x[right]=dmax
7       for ( 1 ≤ j < left, right < j ≤ n )
8           d.remove( | x[ j ] - dmax | );
9       found = place( x, d, n, left, right - 1 );
10  }
11  if ( found ) // Backtrack
12      for ( 1 ≤ j < left, right < j ≤ n ) // Undo the deletion
13          d.insert( | x[ j ] - dmax | );
14  }
    // If first attempt failed, try to see if setting
    // x[left] = x[n] - dmax is feasible.
15  if ( !found && ( | x[n] - dmax | ∈ d )
16      for all 1 ≤ j < left and right < j ≤ n )
17  {
18      x[ left ] = x[ n ] - dmax;    // Same logic as before
19      for ( 1 ≤ j < left, right < j ≤ n )
20          d.remove( | x[ n ] - dmax - x[ j ] | );
21      found = place( x, d, n, left + 1, right );
22  }
23  if ( found ) // Backtrack
24      for ( 1 ≤ j < left, right < j ≤ n ) // Undo the deletion
25          d.insert( | x[ n ] - dmax - x[ j ] | );
26  }
27  return found;
28 }
```

Figure 10.66 Turnpike reconstruction algorithm: backtracking steps (pseudocode)