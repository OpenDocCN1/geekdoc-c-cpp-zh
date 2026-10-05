# 10.8 Projects

**10.6** Under what conditions ISAM be more efficient than a B+-tree implementation?

**10.7** Prove that the number of leaf nodes in a 2-3 tree with height $k$ is between $2^k-1$ and $3^k-1$.

**10.8** Show the result of inserting the values 55 and 46 into the 2-3 tree of Figure 10.9.

**10.9** You are given a series of records whose keys are letters. The records in the following order: C, S, D, T, A, M, P, I, B, W, N, G, U, R, K, E, H, O, L. Show the 2-3 tree that results from inserting these records.

**10.10** You a series of records whose keys are letters. The records are inserted in the following order: C, S, D, T, A, M, P, I, B, W, N, G, U, R, K, E, H, O, L. Show the tree that results from inserting these records when the 2-3 tree is modified to be $2-3^+$; that is, the internal nodes act only as placeholders. Assume the leaf nodes are capable of holding up to two records.

**10.11** Show the result of inserting the value 55 into the B-tree of Figure 10.17.

**10.12** Show the result of inserting values 1, 2, 3, 4, 5, and 6 (in order) into the $B^+$-tree of Figure 10.18.

**10.13** Show the result of deleting the values 18, 19, and 20 (in order) from the $B^+$-tree of Figure 10.24b.

**10.14** You are given a series of records whose keys are letters. The records are inserted in the following order: C, S, D, T, A, M, P, I, B, W, N, G, U, R, K, E, H, O, L. Show the $B^+$-tree of order four that results from inserting these records. Assume the leaf nodes are capable of storing up to three records.

**10.15** Assume that you have a $B^+$-tree whose internal nodes can store up to 100 children and leaf nodes can store up to 15 records. What are the minimum and maximum number of records that can be stored by the $B^+$-tree with heights 1, 2, 3, 4, and 5?

**10.16** Assume that you have a $B^+$-tree whose internal nodes can store up to 50 children and leaf nodes can store up to 50 records. What are the minimum and maximum number of records that can be stored by the $B^+$-tree with heights 1, 2, 3, 4, and 5?

# 10.8 Projects

**10.1** Implement a two-level linear index for variable-length records as illustrated by Figures 10.1 and 10.2. Assume that disk blocks are 1024 bytes in length. Records in the database file should typically range between 20 and 200 bytes, including a 4-byte value. Each record of the index file should store a key value and the byte offset in the database file for the first byte of