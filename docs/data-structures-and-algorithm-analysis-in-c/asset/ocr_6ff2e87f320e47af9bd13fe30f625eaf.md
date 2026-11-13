```
explicit HashTable( int size = 101 ) : array( nextPrime( size ) )
{
    numHashFunctions = hashFunctions.getNumberOfFunctions( );
    rehashes = 0;
    makeEmpty( );
}

void makeEmpty( )
{
    currentSize = 0;
    for( auto & entry : array )
        entry.isActive = false;
}
```

# Figure 5.38 Routines to initialize and empty the cuckoo hash table

```
/**
 * Compute the hash code for x using specified function.
 */
int myhash( const AnyType & x, int which ) const
{
    return hashFunctions.hash( x, which ) % array.size( );
}

/**
 * Search all hash function places. Return the position
 * where the search terminates or -1 if not found.
 */
int findPos( const AnyType & x ) const
{
    for( int i = 0; i < numHashFunctions; ++i )
    {
        int pos = myhash( x, i );

        if( isActive( pos ) && array[ pos ].element == x )
            return pos;
    }

    return -1;
}
```

# Figure 5.39 Routines to find the location of an item in the cuckoo hash table and to compute the hash code for a given table