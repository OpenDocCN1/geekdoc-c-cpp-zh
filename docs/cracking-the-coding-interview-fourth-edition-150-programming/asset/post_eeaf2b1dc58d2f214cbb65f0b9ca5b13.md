
# Solutions to Chapter 12 | System Design and Memory Limits

12.5 If you were designing a web crawler, how would you avoid getting into infinite loops? pg 72

# SOLUTION

First, how does the crawler get into a loop? The answer is very simple: when we re-parse an already parsed page. This would mean that we revisit all the links in that page, and this would continue in a circular fashion.

Be careful about what the interviewer considers the "same page". Is it URL or content? One could easily get redirected to a previously crawled page.

So how do we stop visiting an already visited page? The web is a graph-based structure, and we commonly use DFS (depth first search) and BFS (breadth first search) for traversing graphs. We can mark already visited pages the same way that we would in a BFS/DFS.

We can easily prove that this algorithm will terminate in any case. We know that each step of the algorithm will parse only new pages, not already visited pages. So, if we assume we have N number of unvisited pages, then at every step we are reducing N (N-1) by 1. It proves that our algorithm will continue until there are only N steps.

# SUGGESTIONS AND OBSERVATIONS

- This question has a lot of ambiguity. Ask clarifying questions!

- Be prepared to answer questions about coverage.

- What kind of pages will you hit with a DFS versus a BFS?

- What will you do when your crawler runs into a honey pot that generates an infinite subgraph for you to wander about?

# Solutions to Chapter 12 | System Design and Memory Limits

12.6 You have a billion urls, where each is a huge page. How do you detect the duplicate documents? pg 72

# SOLUTION

Observations:

- Pages are huge, so bringing all of them in memory is a costly affair. We need a shorter representation of pages in memory. A hash is an obvious choice for this.

- Billions of urls exist so we don't want to compare every page with every other page (that would be O(n^2)).

Based on the above two observations we can derive an algorithm which is as follows:

- Iterate through the pages and compute the hash table of one.
- Check if the hash value is in the hash table. If it is, throw out the url as a duplicate. If it is not, keep the url and insert it into the hash table.

This algorithm will provide us a list of unique urls. But wait, can this fit on one computer?

- How much space does each page take up in the hash table?
- Each page takes up roughly 34 bytes.
- Each url is an average of 30 characters, so that's another 30 bytes at least.
- Each url takes up roughly 34 bytes.

34 bytes * 1 billion = 31.6 gigabytes. We're going to have trouble holding that all in memory!

What do we do?

- We could split this up into files. We'll have to deal with the file loading/unloading—ugh.
- We could hash to disk. Size wouldn't be a problem, but access time might. A hash table on disk would require a random access read for each character and write to a viewed url. this could take msecs waiting for seek and rotational latencies. Elevator algorithms could eliminate random bounding from track to track.
- Or, we could split this up across machines, and deal with network latency. Let's go with this solution, and assume we have n machines.
- First, we hash the document to get a hash value v
- v%n tells us which machine this document's hash table can be found.
- v/n is the value in the hash table that is located on its machine.

# Solutions to Chapter 12 | System Design and Memory Limits

12.7 You have to design a database that can store terabytes of data. It should support efficient range queries. How would you do it?

# SOLUTION

Construct an index for each field that requires range queries. Use a B+ tree to implement the index. A B+ tree organizes sorted data for efficient insertion, retrieval and removal of records. Each record is identified by a key (for this problem, it is the field value). Since it is a dynamic, multilevel index, finding the beginning of the range depends only on the height of the tree, which is usually quite small. Record references are stored in the leaves, sorted by the key. Additional records can be found by following a next block reference. Records will be sequentially available until the key value reaches the maximum value specified in the query. Thus, runtimes will be dominated by the number of elements in a range.

Avoid using trees that store data at interior nodes, as traversing the tree will be expensive since it won't be resident in memory.

# Solutions to Chapter 13 | C++

13.1 Write a method to print the last K lines of an input file using C++.

# SOLUTION

One brute force way would be to count the number of lines (N) and then print from N-10 to Nth line. But, this requires two reads of the file - potentially very costly if the file is large.

We need a solution which allows us to read just once and be able to print the last K lines. We can create extra space for K lines and then store each set of K lines in the array. So, initially, our array has lines 0 through 9, then 1 through 10, then 2 through 11, etc. (if K = 10). Each time we read a new line, we purge the old line from the array. Instead of shifting the array each time (very inefficient), we will use a circular array. This will allow us to always find the last element in O(1) time.

Example of inserting elements into a circular array:

- step 1 (initially): array = {a, b, c, d, e, f}; p = 0
- step 2 (insert g): array = {g, b, c, d, e, f}; p = 1
- step 3 (insert h): array = {g, h, c, d, e, f}; p = 2
- step 4 (insert i): array = {g, h, i, d, e, f}; p = 3

Code:

```cpp
1 string L[K];
2 int lines = 0;
3 while (file.good()) {
4 getline(file, L[lines % K]); // read file line by line
5 ++lines;
6 }
7 // if less than K lines were read, print them all
8 int start, count;
9 if (lines < K) {
10 start = 0;
11 count = lines;
12 } else {
13 start = lines % K;
14 count = K;
15 }
16 for (int i = 0; i < count; ++i) {
17 cout << L[(start + i) % K] << endl;
18 }
```

# OBSERVATIONS AND SUGGESTIONS:

Note, if you do printf(index + i) % K); when there are %s, bad things will happen.

# Solutions to Chapter 13 | C++

13.2 Compare and contrast a hash table vs. STL map. How is a hash table implemented? If the number of inputs is small, what data structure options can be used instead of hash table?

# SOLUTION

Compare and contrast Hash Table vs. STL map

In a hash table, a value is stored by applying hash function on a key. Thus, values are not stored in hash table in sorted order. Additionally, since hash tables use the key to find the index that will store the value, an insert/lookup can be done in amortised O(1) time (assuming only a few collisions in the hashtable). One must handle potential collisions in the hashtable.

In an STL map, insertion of key/value pair is in sorted order of key. It uses a tree to store values, which is why an O(log n) insert/lookup is required. There is also no need to handle collisions. An STL map works well for things like:

- find min element
- find max element
- print elements in sorted order
- find the exact element or, if the element is not found, find the next smallest element

How is a hash table implemented?

1. A good hash function is required (e.g.: operation % prime number) to ensure that the hash values are uniformly distributed.
2. A collision resolving method is also needed: chaining (good for dense table entries), probing (good for sparse table entries), etc.
3. Implement methods to dynamically increase or decrease the hash table size on a given criterion. For example, when the [number of elements] by [table size] ratio is greater than the fixed threshold, increase the hash table size by creating a new hash table and transfer the entries from the old table to the new table by computing the index using new hash function.

What can be used instead of a hash table, if the number of inputs is small?

You can use an STL map. Although this takes O(log n) time, since the number of inputs is small, this time is negligible.
