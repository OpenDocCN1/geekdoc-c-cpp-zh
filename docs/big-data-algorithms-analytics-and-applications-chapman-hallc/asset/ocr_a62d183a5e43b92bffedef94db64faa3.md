![](bbox=[0.05, 0.08, 0.95, 0.32])

# FIGURE 1.2 (a) Metric inverted file. (b) Prefix permutation index. (c) Neighborhood approximation.

list of the objects (saved in the inverted list). After checking the inverted lists of all the reference points, the objects are sorted based on their accumulator value. Objects with a small accumulator value are more similar to the query. Later, the authors of Reference 19 proposed a distributed implementation of the MIF.

# 1.3.2 Brief Permutation Index

To decrease the memory usage, the authors of Reference 20 proposed the brief permutation index. The algorithm proposes a smaller representation of the ordered lists in order to save memory. After generating the ordered lists L(o_i,R), each list is encoded using a fixed-size bit string. Once a query is received, its order list is also encoded in the same way and compared with the vectors using the binary Hamming distances [21]. In Reference 22, the authors proposed a variation with LSH, but the recall drops when the speed increases.

# 1.3.3 Prefix Permutation Index

In Reference 23, the authors proposed a new technique called the prefix permutation index (PP-index). The algorithm aims to decrease the memory usage by reducing the number of references and performing some direct distance calculation (DDC) with a portion from the database. PP-index only stores a prefix of the permutations of length l (where l < n) in the main memory in a trie tree, and the data objects are saved in blocks on the hard disk. Objects that share the same prefix are saved close to each other. Figure 1.2b shows the PP-index for the partial ordered lists in Figure 1.1c. Once a query is submitted, all the objects in the block sharing the same prefix are ranked based on their distance to the query. The PP-index requires less memory than the previous data structures and uses the permutation prefix in order to quickly retrieve the relevant objects, in a hash-like manner. The proposed technique initially gives a lower recall value. An improvement is made using multiple queries. When a query is received, the permutation list for the query is computed. Different combinations of the query permutation list are then submitted to the tree as new queries.

# 1.3.4 Neighborhood Approximation

In Reference 16, the authors proposed neighborhood approximation (NAPP). The main idea of the NAPP is to get the objects that are located in the intersection region of reference objects shared between the query and database objects. Hence, if there is a query q,