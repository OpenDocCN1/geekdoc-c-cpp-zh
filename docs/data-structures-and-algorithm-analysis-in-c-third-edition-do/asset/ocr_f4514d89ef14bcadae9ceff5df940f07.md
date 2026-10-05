Sec. 9.5 Further Reading

345

seems like a small increase

Two possible solutions to this problem are

+   1. Do a local reorganization upon deletion to try to shorten the average path
length. For example, after deleting a key, continue to follow the probe se-
ence of key and swap records down the probe sequence into
t slot of the deleted record (being careful not to remove any key
from its probe sequence). This will not work for all collision resolution poli-

+   2. Periodically rehash the table by reinserting all records into a new hash table.
Not only will this remove thebstones, but it also provides an opportunity
to place the most frequently accessed records into their home positions.

# 9.5 Further Reading

For a comparison of the efficiencies for various self-organizing techniques, see
Bentley and McGeoch,"Amortized Analysis of Self-Organizing Sequential Search
Heuristics" [BM85]. The text compression expression of Section 9.2 comes from
Bentley et al., "A Locally Data Compression Scheme" [BST86]. For
 on Siv-Lempel coding, see Data Compression: Methods and Theory by
James A. Stoer [Sto88]. Knuth covers self-organizing lists and Zipf distributions
in Volume 3 of The Art of Computer Programming[Knu98].

Introduction to Modern Information Retrieval by Salton and McGill [SM83] is
an excellent source for more information about document retrieval techniques.

See the paper "Practical Minimal Hash Functions for Large Databases"
by Fox et al [FHCD92] for an introduction and a good algorithm for perfect hash-
ing.

For details on the various collision resolution policies, see
Knuth, Volume 3 [Knu98] and Concrete Mathematics: A Foundation for Computer
Science by Graham, Knuth, and Patashnik [GKP94].

The modeling of hashing presented in this chapter has a fixed-size hash
table. A problem not addressed is what to do when the hash table gets half full and
 records must be inserted. This is the domain of dynamic hashing methods.
A good introduction to this topic is "Dynamic Hashing Schemes" by R.J. Embody
 H.C. Du [ED88].

# 9.6 Exercises

+   9.1 Create a graph showing expected cost versus the probability of an unsuc-\cessful search when performing sequential search (see Section 9.1). What