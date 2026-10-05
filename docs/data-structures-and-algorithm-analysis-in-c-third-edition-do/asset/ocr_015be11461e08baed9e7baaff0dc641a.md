a function Transpose that takes as input a value to be searched for and which adjusts the list appropriately. If the value is not already in the list, add it to the end of the list.

**9.11** Write functions for computing union, intersection, and set difference on arbitrary bit vectors used to represent set membership as described in Section 9.3. Assume that for each operation both vectors are of equal length.

**9.12** Compute the probabilities for the following situations. These probabilities can be computed analytically, or you may write a computer program to generate them by simulation.

+   (a) Out of a group of 23 students, what is the probability that 2 students share the same birthday?

+   (b) Out of a group of 100 students, what is the probability that 3 students share the same birthday?

+   (c) How many students must be in the class for the probability to be at least 50% that there are 2 share a birthday in the same month?

**9.13** Assume that you are hashing $K$ to a hash table of $n$ slots (indexed from 0 to $n-1$). For each of the functions $h(K)$, is the function acceptable a hash function (i.e., would the program work correctly for both insertions and searches), and if so, is it a good hash function? **Random (n)** returns a random integer between 0 and $n-1$, inclusive.

+   (a) $h(k) = k/n$ where $k$ and $n$ are integers.

+   (b) $h(k) = 1$.

+   (c) $h(k) = (k + \text{Random}(n)) \bmod n$.

+   (d) $h(k) = k \bmod n$ where $n$ is a prime number.

**9.14** Assume that you have a seven-slot closed hash table (the slots are numbered 0 through 6). Show the final hash table that would result if you used the hash function $h(k) = k \bmod 7$ and linear probing on this list of numbers: 3, 12, 9, 2, 7. After inserting the record with key value 2, for each empty slot the probability that it will be the next one filled.

**9.15** Assume that you have a ten-slot closed hash table (the slots are numbered 0 through 9). Show the final hash table that would result if you used the hash function $h(k) = k \bmod 10$ and quadratic probing on this list of numbers: 3, 12, 9, 2, 79, 44. After inserting the record with key value 46, for each empty slot the probability that it will be the next one filled.

**9.16** Assume that you have a ten-slot closed hash table (the slots are numbered 0 through 9). Show the final hash table that would result if you used the hash function $h(k) = k \bmod 10$ and pseudo-random probing on this list of numbers: 3, 12, 9, 2, 79, 44. The permutation of offsets to be used by the pseudo-random probing will be: 5, 9, 2, 1, 4, 8, 6, 3, 7. After inserting the record with key value 44, for each empty slot the probability that it will be the next filled.