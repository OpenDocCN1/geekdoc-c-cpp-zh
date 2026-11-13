```
1 // Returns true if word1 and word2 are the same length
2 // and differ in only one character.
3 bool oneCharOff( const string & word1, const string & word2 )
4 {
5     if( word1.length( ) != word2.length( ) )
6         return false;
7
8     int diffs = 0;
9
10    for( int i = 0; i < word1.length( ); ++i )
11        if( word1[ i ] != word2[ i ] )
12            if( ++diffs > 1 )
13                return false;
14
15    return diffs == 1;
16 }
```

# Figure 4.70 Routine to check if two words differ in only one character

```
1 // Computes a map in which the keys are words and values are vectors of words
2 // that differ in only one character from the corresponding key.
3 // Uses a quadratic algorithm.
4 map<string,vector<string>> computeAdjacentWords( const vector<string> & words )
5 {
6     map<string,vector<string>> adjWords;
7
8     for( int i = 0; i < words.size( ); ++i )
9         for( int j = i + 1; j < words.size( ); ++j )
10            if( oneCharOff( words[ i ], words[ j ] ) )
11            {
12                adjWords[ words[ i ] ].push_back( words[ j ] );
13                adjWords[ words[ j ] ].push_back( words[ i ] );
14            }
15
16    return adjWords;
17 }
```

# Figure 4.71 Function to compute a map containing words as keys and a vector of words that differ in only one character as values. This version runs in 1.5 minutes on an 89,000-word dictionary.

store each collection, and the same idiom applies. The code is shown in Figure 4.72. Line 8 shows the declaration for the second map, lines 11 and 12 populate the map, and then an extra loop is used to iterate over each group of words. Compared to the first algorithm, the second algorithm is only marginally more difficult to code and runs in 18 seconds, or about six times as fast.