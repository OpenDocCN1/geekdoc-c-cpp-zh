![](bbox=[0.05, 0.08, 0.8, 0.38])

Figure 10.64 Decision tree for the worked turnpike reconstruction example

```
bool turnpike( vector<int>& x, DistSet d, int n )
{
    x[1] = 0;
    d.deleteMax( x[ n ] );
    d.deleteMax( x[ n - 1 ] );
    if( x[ n ] - x[ n - 1 ] == d )
    {
        d.remove( x[ n ] - x[ n - 1 ] );
        return place( x, d, n, 2, n - 2 );
    }
    else
        return false;
}
```

Figure 10.65 Turnpike reconstruction algorithm: driver routine (pseudocode)

pass the same arguments plus the boundaries Left and Right. xLeft,...,xRight are the x coordinates of points that we are trying to place. If D is empty (or Left > Right), then a solution has been found, and we can return. Otherwise, we first try to place xRight = Dmax. If all the appropriate distances are present (in the correct quantity), then we tentatively place this point, remove these distances, and try to fill from Left to Right - 1. If the distances are not present, or the attempt to fill Left to Right - 1 fails, then we try setting xLeft = xN - dmax, using a similar strategy. If this does not work, then there is no solution; otherwise a solution has been found, and this information is eventually passed back to turnpike by the return statement and x array: