```
1 /**
2  * Rehashing for quadratic probing hash table.
3  */
4 void rehash( )
5 {
6     vector<HashEntry> oldArray = array;
7
8     // Create new double-sized, empty table
9     array.resize( nextPrime( 2 * oldArray.size( ) ) );
10    for ( auto & entry : array )
11        entry.info = EMPTY;
12
13    // Copy table over
14    currentSize = 0;
15    for ( auto & entry : oldArray )
16        if ( entry.info == ACTIVE )
17            insert( std::move( entry.element ) );
18 }
19
20 /**
21  * Rehashing for separate chaining hash table.
22  */
23 void rehash( )
24 {
25    vector<list<HashedObj>> oldLists = theLists;
26
27    // Create new double-sized, empty table
28    theLists.resize( nextPrime( 2 * theLists.size( ) ) );
29    for ( auto & thisList : theLists )
30        thisList.clear( );
31
32    // Copy table over
33    currentSize = 0;
34    for ( auto & thisList : oldLists )
35        for ( auto & x : thisList )
36            insert( std::move( x ) );
37 }
```

Figure 5.22 Rehashing for both separate chaining hash tables and probing hash tables

also be instantiated with a function object that provides (or overrides a default) comparison function, unordered_set and unordered_map can be instantiated with function objects that provide a hash function and equality operator. Thus, for example, Figure 5.23 illustrates how an unordered set of case-insensitive strings can be maintained, assuming that some string operations are implemented elsewhere.