# Linpack_Bench

```
{
    if ( dmax < fabs ( dx[i] ) )
    {
        value = i + 1;
        dmax = fabs ( dx[i] );
    }
}
else
{
    ix = 0;
    dmax = fabs ( dx[0] );
    ix = ix + incx;

    for ( i = 1; i < n; i++) {
        if ( dmax < fabs ( dx[ix] ) )
        {
            value = i + 1;
            dmax = fabs ( dx[ix] );
        }
        ix = ix + incx;
    }

    return value;
}
```

**********************************************************************/

```
double r8_epsilon ( )
```

**********************************************************************/*

Purpose:

R8_EPSILON is a number R which is a power of 2 with the
property that

Discussion:

Licensing:

This code is distributed under the GNU LGPL license.

Modified: