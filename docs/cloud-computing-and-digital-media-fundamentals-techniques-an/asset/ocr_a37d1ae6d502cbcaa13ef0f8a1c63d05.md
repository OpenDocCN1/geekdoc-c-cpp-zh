# 228 ■ Cloud Computing and Digital Media

![](bbox=[0.137, 0.097, 0.862, 0.358])

Figure 9.11 Predicate-oriented prefix tree storage of RDF data: Top-5 largest Predicate files from the Billion Triple Challenge 2009.

When there come new updates, the updated strategy is as follows. First, locate the block for new update by checking its *Predicate*. If the *Predicate* can be interpreted in the prefix tree directory, locate the directory and further refer to the data blocks from both the Subject- and Object-sorted list. If the *Predicate* indicates that this belongs to a small predicate file, search the B+ tree to locate a data block containing triples with the same *Predicate* value. After, the data storage block is identified, just append the update to the original records until certain threshold is met. When a data block must split, scanning and sorting are performed to guarantee the range integrity of new blocks. The update of corresponding block-level index is an in-memory operation, and therefore can be done very efficiently.

# 9.4.7 Related Work

There are mainly two categories of solutions for RDF management and query processing. One is to use traditional relational database management system (RDBMS) technologies, either stand-server or distributed (parallel) computing framework. RDF data are represented as tables in databases. Intensive research interests lies in RDF decomposition (SW-Store [50]) or composition (property table [51]), index building and searching (Hexastore [49], RDF-3X [48]), and query optimization [43]. However, due to the limitation of RDBMS's scalability, the above solutions