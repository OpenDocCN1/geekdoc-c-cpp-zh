
Assuming that the size of P is less than T (and usually it is significantly less), then we would reasonably expect that the time to solve this problem for a given P and T would be at least linear in the length of T, and in fact there are several O( |T| ) algorithms.

However, we are interested in a more common problem, in which T is fixed, and queries with different P occur frequently. For instance, T could be a huge archive of email messages, and we are interested in repeatedly searching the email messages for different patterns. In this case, we are willing to preprocess T into a nice form that would make each individual search much more efficient, taking time significantly less than linear in the size of T—either logarithmic in the size of T, or even better, independent of T and dependent only on the length of P.

One such data structure is the suffix array and suffix tree (that sounds like two data structures, but as we will see, they are basically equivalent, and trade time for space).

## 12.4.1 Suffix Arrays

A suffix array for a text, T, is simply an array of all suffixes of T arranged in sorted order. For instance, suppose our text string is banana. Then the suffix array for banana is shown in Figure 12.21.

A suffix array that stores the suffixes explicitly would seem to require quadratic space, since it stores one string of each length 1 to N (where N is the length of T). In C++, this is not exactly true, since in C++ we can use the primitive null-terminated char array character representation of strings, and in that case, a suffix is specified by a char * that points at the first character of the substring. Thus, the same array of characters is shared, and the additional memory requirement is only the char * pointer for the new substring. Nonetheless, using a char * is highly C or C++-dependent; thus it is common for a practical implementation to store only the starting indices of the suffixes in the suffix array, which is much more language independent. Figure 12.22 shows the indices that would be stored.

| Index | Suffix |
| :--- | :--- |
| 0 | a |
| 1 | ana |
| 2 | anana |
| 3 | banana |
| 4 | na |
| 5 | nana |

Figure 12.21 Suffixes for “banana”

| | Index | Substring Being Represented |
|---|---|---|
| 0 | 5 | a |
| 1 | 3 | ana |
| 2 | 1 | anana |
| 3 | 0 | banana |
| 4 | 4 | na |
| 5 | 2 | nana |

Figure 12.22 Suffix array that stores only indices (full substrings shown for reference)

We can also use the suffix array to find the number of occurrences of P. They will be stored sequentially in the suffix array, thus two binary searches suffice to find a range of suffixes that will be guaranteed to begin with P. One way to speed this search is to compute the longest common prefix (LCP) for each consecutive pair of substrings; if this computation is done as the suffix array is built, then each query to find the number of occurrences of P can be sped up to O( |P| + log|T| ) although this is not obvious. Figure 12.23 shows the LCP computed for each substring, relative to the preceding substring.

The longest common prefix also provides information about the longest pattern that occurs twice in the text: Look for the largest LCP value, and take that many characters of the corresponding substring. In Figure 12.23, this is 3, and the longest repeated pattern is ana.

| | Index | LCP | Substring Being Represented |
|---|---|---|---|
| 0 | 5 | - | a |
| 1 | 3 | 1 | ana |
| 2 | 1 | 3 | anana |
| 3 | 0 | 0 | banana |
| 4 | 4 | 0 | na |
| 5 | 2 | 2 | nana |

Figure 12.23 Suffix array for "banana"; includes longest common prefix (LCP)

Figure 12.24 shows simple code to compute the suffix array and longest common prefix information for any string. Line 26 obtains a primitive (char *) string from str, and lines 28 to 31 obtain the suffixes by computing and storing these pointers using pointer arithmetic (line 31). At lines 33 and 34, the suffixes are sorted, the code at line 34 represents the C++11 lambda feature, in which the 'less than' function that is needed for two char * types is provided as the third parameter to sort, without the need to write a named function. Lines 36 and 37 compute the suffixes' starting indices using pointer arithmetic, and lines 39 to 41 compute the longest common prefixes for adjacent entries by calling the computeLCP routine written at lines 4 to 12.

```
1 /*
2  * Returns the LCP for any two strings
3  *
4 int computeLCP( const string & s1, const string & s2 )
5 {
6  int i = 0;
7
8  while ( i < s1.length() && i < s2.length() && s1[ i ] == s2[ i ] )
9  ++i;
10

11 return i;
12 }
13 
14 /*
15  * Fill in the suffix array and LCP information for String str
16  * str is the input String
17  * SA is an existing array to place the suffix array
18  * LCP is an existing array to place the LCP information
19  *
20 void createSuffixArraysSlow( const string & str, vector<int> & SA, vector<int> & LCP )
21 {
22  if( SA.size() != str.length() || LCP.size() != str.length() )
23  throw invalid_argument( "Mismatched vector sizes" );
24

25 size_t N = str.length();
26 const char *cstr = str.c_str();
27

28 vector<const char *> suffixes( N );
29

30 for( int i = 0; i < N; ++i )
31 suffixes[ i ] = cstr + i;
32

33 std::sort( begin( suffixes ), end( suffixes ),
34  [ ] ( const char *s1, const char *s2 ) { return strcmp( s1, s2 ) < 0; } );
35

36 for( int i = 0; i < N; ++i )
37 SA[ i ] = suffixes[ i ] - cstr;
38

39 LCP[ 0 ] = 0;
40 for( int i = 1; i < N; ++i )
41 LCP[ i ] = computeLCP( suffixes[ i - 1 ], suffixes[ i ] );
42 }
```

Figure 12.24 Simple algorithm to create suffix array and LCP array

The running time of the suffix array computation is dominated by the sorting step, which uses O(N log N) comparisons. In many circumstances this can be reasonably acceptable performance. For instance, a suffix array for a 3,000,000-character English-language novel can be built in just a few seconds. However, the O(N log N) cost, based on the number of comparisons, hides the fact that a String comparison between s1 and s2 takes time that depends on LCP(s1, s2). So while it is true that almost all these comparisons end quickly when run on the suffixes found in natural language processing, the comparisons will be expensive in applications where there are many long common substrings. One such example occurs in pattern searching of DNA, whose alphabet consists of four characters (A, C, G, T) and whose strings can be huge. For instance, the DNA string for human chromosome 22 has roughly 35 million characters, with a maximum LCP of approximately 200,000 and an average LCP of nearly 2,000. And even the HTML/Java distribution for JDK 1.3 (much smaller than the current distribution) is nearly 70 million characters, with a maximum LCP of roughly 37,000 and an average LCP of roughly 14,000. In the degenerate case of a String that contains only one character, repeated N times, it is easy to see that each comparison takes O(N) time, and the total cost is O(N^2 log N).

In Section 12.4.3, we will show a linear-time algorithm to construct the suffix array.

## 12.4.2 Suffix Trees

Suffix arrays are easily searchable by binary search, but the binary search itself automatically implies log T cost. What we would like to do is find a matching suffix even more efficiently. One idea is to store the suffixes in a trie. A binary trie was seen in our discussion of Huffman codes in Section 10.1.2.

The basic idea of the trie is to store the suffixes in a tree. At the root, instead of having two branches, we would have one branch for each possible first character. Then at the next level, we would have one branch for the next character, and so on. At each level we are doing multiway branching, much like radix sort, and thus we can find a match in time that would depend only on the length of the match.

In Figure 12.25, we see on the left a basic trie to store the suffixes of the string deed. These suffixes are d, deed, ed, and eed. In this trie, internal branching nodes are drawn in circles, and the suffixes that are reached are drawn in rectangles. Each branch is labeled with the character that is chosen, but the branch prior to a completed suffix has no label.

This representation could waste significant space if there are many nodes that have only one child. Thus in Figure 12.25, we see an equivalent representation on the right, known as a compressed trie. Here, single-branch nodes are collapsed into a single node. Notice that although the branches now have multicharacter labels, all the labels for the branches of any given node must have unique first characters. Thus, it is still just as easy as before to choose which branch to take. Thus we can see that a search for a pattern, P, depends only on the length of the pattern P as desired. (We assume that the letters of the alphabet are represented by numbers 1, 2, ... . Then each node stores an array representing each possible branch and we can locate the appropriate branch in constant time. The empty edge label can be represented by 0.)

If the original string has length N, the total number of branches is less than 2N. However, this by itself does not mean that the compressed trie uses linear space: The labels on the edges take up space. The total length of all the labels on the compressed
