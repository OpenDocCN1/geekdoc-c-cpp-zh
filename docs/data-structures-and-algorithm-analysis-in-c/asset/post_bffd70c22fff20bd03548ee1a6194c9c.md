
```cpp
template <typename AnyType, typename HashFamily>
class CuckooHashTable
{
  public:
    explicit CuckooHashTable( int size = 101 );

    void makeEmpty( );
    bool contains( const AnyType & x ) const;

    bool remove( const AnyType & x );
    bool insert( const AnyType & x );
    bool insert( AnyType && x );

  private:
    struct HashEntry
    {
      AnyType element;
      bool isActive;

      HashEntry( const AnyType & e = AnyType{ }, bool a = false )
        : element{ e }, isActive{ a } { }
      HashEntry( AnyType && e, bool a = false )
        : element{ std::move( e ) }, isActive{ a } { }
    };

    bool insertHelper1( const AnyType & xx );
    bool insertHelper1( AnyType && xx );
    bool isActive( int currentPos ) const;

    size_t myhash( const AnyType & x, int which ) const;
    int findPos( const AnyType & x ) const;
    void expand( );
    void rehash( );
    void rehash( int newSize );

    static const double MAX_LOAD = 0.40;
    static const int ALLOWED_REHASHES = 5;

    vector<HashEntry> array;
    int currentSize;
    int numHashFunctions;
    int rehashes;
    UniformRandom r;
    HashFamily hashFunctions;
  };
```

### Figure 5.37 Class interface for cuckoo hashing

```cpp
explicit CuckooHashTable( int size = 101 ) : array( nextPrime( size ) )
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

### Figure 5.38 Routines to initialize and empty the cuckoo hash table

```cpp
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

### Figure 5.39 Routines to find the location of an item in the cuckoo hash table and to compute the hash code for a given table

```cpp
/**
 * Return true if x is found.
 */
bool contains( const AnyType & x ) const
{
    return findPos( x ) != -1;
}
```

### Figure 5.40 Routine to search a cuckoo hash table

```cpp
/**
 * Remove x from the hash table.
 * Return true if item was found and removed.
 */
bool remove( const AnyType & x )
{
    int currentPos = findPos( x );
    if( !isActive( currentPos ) )
        return false;

    array[ currentPos ].isActive = false;
    --currentSize;

    return true;
}
```

### Figure 5.41 Routine to remove from a cuckoo hash table

```cpp
bool insert( const AnyType & x )
{
    if( contains( x ) )
        return false;

    if( currentSize == array.size( ) * MAX_LOAD )
        expand( );

    return insertHelper1( x );
}
```

### Figure 5.42 Public insert routine for cuckoo hashing

Our basic logic is different from the classic scheme. We have already tested that the item to insert is not already present. At lines 15 to 25, we check to see if any of the valid positions are empty; if so, we place our item in the first available position and we are done. Otherwise, we evict one of the existing items. However, there are some tricky issues:

```cpp
1  static const int ALLOWED_REHASHES = 5;
2
3  bool insertHelper1( const AnyType & xx )
4  {
5      const int COUNT_LIMIT = 100;
6      AnyType x = xx;
7
8      while ( true )
9      {
10         int lastPos = -1;
11         int pos;
12
13         for( int count = 0; count < COUNT_LIMIT; ++count )
14         {
15             for( int i = 0; i < numHashFunctions; ++i )
16             {
17                 pos = myhash( x, i );
18
19                 if( isActive( pos ) )
20                 {
21                     array[ pos ] = std::move( HashEntry{ std::move( x ), true } );
22                     ++currentSize;
23                     return true;
24                 }
25             }
26         }
27
28         // None of the spots are available. Evict a random one
29         int i = 0;
30         do
31         {
32             pos = myhash( x, r.nextInt( numHashFunctions ) );
33         } while( pos == lastPos && ++i < 5 );
34
35         lastPos = pos;
36         std::swap( x, array[ pos ].element );
37     }
38
39     if( ++rehashes > ALLOWED_REHASHES )
40     {
41         expand( ); // Make the table bigger
42         rehashes = 0; // Reset the # of rehashes
43     }
44     else
45         rehash( ); // Same table size, new hash functions
46 }
```

### Figure 5.43 Insertion routine for cuckoo hashing uses a different algorithm that chooses the item to evict randomly, attempting not to re-evict the last item. The table will attempt to select new hash functions (rehash) if there are too many evictions and will expand if there are too many rehashes.

- Evicting the first item did not perform well in experiments.
- Evicting the last item did not perform well in experiments.
- Evicting the items in sequence (i.e., the first eviction uses hash function 0, the next uses hash function 1, etc.) did not perform well in experiments.
- Evicting the item purely randomly did not perform well in experiments: In particular, with only two hash functions, it tended to create cycles.

To alleviate the last problem, we maintain the last position that was evicted, and if our random item was the last evicted item, we select a new random item. This will loop forever if used with two hash functions, and both hash functions happen to probe to the same location, and that location was a prior eviction, so we limit the loop to five iterations (deliberately using an odd number).

The code for expand and rehash is shown in Figure 5.44. expand creates a larger array but keeps the same hash functions. The zero-parameter rehash leaves the array size unchanged but creates a new array that is populated with newly chosen hash functions.

```cpp
1 void expand() {
2   {
3     rehash( static_cast<int>( array.size( ) / MAX_LOAD ) );
4   }
5 }
6
7 void rehash( )
8 {
9   hashFunctions.generateNewFunctions( );
10  rehash( array.size( ) );
11 }
12
13 void rehash( int newSize )
14 {
15   vector<HashEntry> oldArray = array;
16
17   // Create new double-sized, empty table
18  array.resize( nextPrime( newSize ) );
19   for( auto & entry : array )
20     entry.isActive = false;
21
22   // Copy table over
23   currentSize = 0;
24   for( auto & entry : oldArray )
25     if( entry.isActive )
26       insert( std::move( entry.element ) );
27 }
```

### Figure 5.44 Rehashing and expanding code for cuckoo hash tables

```cpp
template <int count>
class StringHashFamily
{
public:
    StringHashFamily() : MULTIPLIERS( count )
    {
        generateNewFunctions( );
    }
    int getNumberOfFunctions( ) const
    {
        return count;
    }
private:
    void generateNewFunctions( )
    {
        for( auto & mult : MULTIPLIERS )
            mult = r.nextInt( );
    }
    size_t hash( const string & x, int which ) const
    {
        const int multiplier = MULTIPLIERS[ which ];
        size_t hashVal = 0;
        for( auto ch : x )
            hashVal = multiplier * hashVal + ch;
        return hashVal;
    }
private:
    vector<int> MULTIPLIERS;
    UniformRandom r;
};
```

### Figure 5.45 Casual string hashing for cuckoo hashing; these hash functions do not provably satisfy the requirements needed for cuckoo hashing but offer decent performance if the table is not highly loaded and the alternate insertion routine in Figure 5.43 is used.

Finally, Figure 5.45 shows the StringHashFamily class that provides a set of simple hash functions for strings. These hash functions replace the constant 37 in Figure 5.4 with randomly chosen numbers (not necessarily prime).

The benefits of cuckoo hashing include the worst-case constant lookup and deletion times, the avoidance of lazy deletion and extra data, and the potential for parallelism.
