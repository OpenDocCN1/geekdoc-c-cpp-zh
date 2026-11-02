technique widely used in pattern recognition, particularly oriented to temporal distortions between vectors, such as the time of writing, speed of video camera, the omission of a letter, etc. These temporal variations are not proportional and vary accordingly to each person, object or event, and those situations are not repetitive in any aspects. DTW uses dynamic programming to find similarities and differences between two or more vectors.

This method considers two sequences representing feature vectors defined by a(i), i=1,2,...,l and b(j), j=1,2,...,J, where, in general, the number of elements differs in each vector (l≠J). The aim of DTW is to find an appropriate distance between the two sequences and in a two-dimensional plane, where each sequence represents one axis, and each point corresponds to the local relationship between two sequences. The nodes (i,j) of the plane are associated with a cost that is defined by the function d(i,j)=d(i,j)=|a(i)-b(j)|, which represents the distance between the elements a(i) and b(j).

The collection of points begins in the starting point (i0j0) and finishes in the (iJjJ) nodes, and it being an ordered pair of size k, where k is the number of nodes along the way. Every path established with the points is associated with a total cost D and defined by

D = Σ_{k=0}^{k-1} d(i_k , j_k). (19)

and the distance between the two sequences is defined as the minimum value D of all the possible paths

D(a,b)= min_k (D). (20)

There are normalization and temporary limitations in the search for the minimum distance between patterns to compare [22], [1]. These limitations are: endpoint, monotonicity conditions, local continuity, global path and slope weight.

The final point is bounded by the size of windowing and performed in each pattern, at most cases is empirical and defined to extremes, that is:

i(1)=1, j(1)=1

i(K)=I, j(K)=J. (21)

Figure 3 shows an example in which it is only partially considered one of the sequences, a situation that is not allowed to search the minimum cost.

The monotonicity conditions try to maintain the temporal order of the normalization of the time, and avoid negative slopes, by

i_{k+1} ≥ i_k (22)

and

j_{k+1} ≥ j_k. (23)