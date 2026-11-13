the second character of the four-letter word group, with a new map, and then the third character, and finally the fourth character.

The general outline is

```
for each group g, containing words of length len
  for each position p (ranging from 0 to len-1)
  {
    Make an empty map<string,vector<string>> repsToWords
    for each word w
    {
      Obtain w's representative by removing position p
      Update repsToWords
    }
    Use cliques in repsToWords to update adjWords map
  }
```

Figure 4.73 contains an implementation of this algorithm. The running time improves to two seconds. It is interesting to note that although the use of the additional maps makes the algorithm faster, and the syntax is relatively clean, the code makes no use of the fact that the keys of the map are maintained in sorted order.

```
// Computes a map in which the keys are words and values are vectors of words
// that differ in only one character from the corresponding key.
// Uses an efficient algorithm that is O(N log N) with a map
map<string,vector<string>> computeAdjacentWords( const vector<string>& words )
{
    map<string,vector<string>> adjWords;
    map<int,vector<string>> wordsByLength;
    // Group the words by their length
    for( auto & str : words )
        wordsByLength[ str.length() ].push_back( str );
    // Work on each group separately
    for( auto & entry : wordsByLength )
    {
        const vector<string>& groupsWords = entry.second;
        int groupNum = entry.first;
        // Work on each position in each group
        for( int i = 0; i < groupNum; ++i )
```

![](bbox=[0.2, 0.86, 0.9, 0.93])