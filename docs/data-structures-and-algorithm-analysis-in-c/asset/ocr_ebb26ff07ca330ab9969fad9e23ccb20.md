```
13 BinomialNode *oldRoot = theTrees[ minIndex ];
14 BinomialNode *deletedTree = oldRoot->leftChild;
15 delete oldRoot;
16
17 // Construct H''
18 BinomialQueue deletedQueue;
19 deletedQueue.theTrees.resize( minIndex + 1 );
20 deletedQueue.currentSize = ( 1 << minIndex ) - 1;
21 for( int j = minIndex - 1; j >= 0; --j )
22 {
23 deletedQueue.theTrees[ j ] = deletedTree;
24 deletedTree = deletedTree->nextSibling;
25 deletedQueue.theTrees[ j ]->nextSibling = nullptr;
26 }
27
28 // Construct H'
29 theTrees[ minIndex ] = nullptr;
30 currentSize -= deletedQueue.currentSize + 1;
31
32 merge( deletedQueue );
33 }
34
35 /**
36 * Find index of tree containing the smallest item in the priority queue.
37 * The priority queue must not be empty.
38 * Return the index of tree containing the smallest item.
39 */
40 int findMinIndex( ) const
41 {
42 int i;
43 int minIndex;
44
45 for( i = 0; theTrees[ i ] == nullptr; ++i )
46 ;
47
48 for( minIndex = i; i < theTrees.size( ); ++i )
49 if( theTrees[ i ] != nullptr &&
50 theTrees[ i ]->element < theTrees[ minIndex ]->element )
51 minIndex = i;
52
53 return minIndex;
54 }
```

Figure 6.56 (continued)