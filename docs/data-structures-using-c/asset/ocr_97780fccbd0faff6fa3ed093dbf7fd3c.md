list are sequential storage media where the data may or may not be ordered. There are two ways for storing the collection of records namely, sequential and non-sequential. For the time being, let us assume that we have a sequential file F, and we wish to retrieve a record with a certain key value k. If F has n records with the key value k, such as i = 1 to n, then one way to carry out the retrieval is by examining the key values in the order of their arrangement until the correct record is located. Such a search is known as sequential search since the records are examined sequentially from the first till the last.

Hence, a sequential search begins with the first available record and proceeds to the next available record repeatedly until we find the target key or conclude that it is not found. Sequential search is also called as linear search.

Algorithm 9.1 depicts the steps involved in sequential search.

+   ALGORITHM 9.1
+   1. Set i = 0, flag = 0
+   2. Compare key[i] and target
+      if(key[i] = target)
+      Set flag = 1, location = i and goto step 5
+   3. Move to next data element
+      i = i + 1
+   4. if(i < n) goto step 2
+   5. if(flag = 1) then
+      return i as position of target located
+      else
+      report as ‘Target not found’
+   6. stop

Figure 9.1 shows a sample sequential unordered data and traces the search for the target data of 89.

| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|---|---|---|
| Elements | 23 | 12 | 9 | 10 | 11 | 89 | 78 | 66 | 88 |

Fig. 9.1 Sequential search for target data of 89

Initially, i = 0 and the target element 89 is to be searched. At each pass, the target 89 is compared with the element at the i th location till it is found or the index i exceeds the size. At i = 5, the search is successful.

Algorithm 9.1 for sequential search is implemented in C++ as shown in Program Code 9.1.