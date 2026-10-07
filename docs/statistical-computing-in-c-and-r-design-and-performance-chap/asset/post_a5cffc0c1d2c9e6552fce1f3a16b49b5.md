
# ADT DICTIONARY

The former returns a list that contains the requested elements from the database thereby making it possible to use the crappy function.

## 9.2.4.4 Pairwise independent and universal hash families

In real life, data may obey some regular pattern or its distribution may contain unknown biases. Our uniform hashing assumption may not be satisfied in such a situation, leading to poor performance. In this section we explain an approach that avoids this problem.

Imagine you are the administrator of a site that uses an open-source program that contains a hash table. The behavior of the hash table and its efficiency depends on the input to the program. A good hash table (and in particular, its hash function) is designed to work well for typical sequences. For example, the results we discussed support the claim that the expected number of steps for a hash table look-up is nearly constant require that the input from a “typical” input sequence. Imagine an adversary whose goal is to disrupt the performance of your program. Knowing your hash function may be able to choose a sequence of keys all hash to the same slot, causing the hash table to perform much efficiently or even causing errors that, with a “typical” input sequence, would be extremely unlikely to happen.

A simple solution to this problem is to avoid specifying the hash function in the code. Instead, choose the hash function randomly from a family of functions that are large and diverse to guarantee a high probability of good behavior on any input. A family H of functions with range {0, ..., m-1} is said to be universal, for every two keys $k_1$ and $k_2$, when $h \in H$ is selected randomly we have $P(h(k_1) = h(k_2)) \le 1/m$. Universal hash families were introduced by Carter and Wegman (1979).

A stronger condition, in a large variety of sets (e.g., randomization of randomized algorithms), is to require for every pair $(k_1, k_2)$ and every pair $(x, y)$ of hash values, $P(h(k)=y) \le 1/m^2$. In other words, every pair of $(h(k_1), h(k_2))$ is equally likely. A family of hash functions is called 2-universal or pairwise independent.

Universal hash families have other interesting and useful properties. For example, if n objects are hashed into a table of size m with the hash function chosen at random from a universal family, then the expected number of collisions per hashed key is no more than 1.

**Theorem 9.1.** Suppose there are n keys in a table of size m with the hash function chosen uniformly at random from a universal family. Then, for every key k,

`E[number of collisions on insertion of k] ≤ 1.`

Proof. For every key $k \neq k'$, the probability that $h(k)=h(k')$ is at most 1/m. The expected number of keys in the table with hash values equal to $k$ is at most $n/m \le 1$.

Efficient hash families are not difficult to demonstrate by the following two.

**Example 9.3.** A frequently used hash function for strings is defined by $h(S) = h(s_1) + h(s_2) + ... + h(s_n) \pmod m$, for the string $S = s_1s_2...s_n$ where $m$ is the size of the hash table and $h$ is a hash function mapping the set of all characters into $\{0,...,m-1\}$. An extension of this idea is to randomly select $N$ functions $h_1,...,h_N$ from the set of all functions mapping the set of characters into $\{0, ..., m-1\}$ and define

`h(S) = h_1(s_1) + h_2(s_2) + ... + h_n(s_n) mod m`

for any string of length $n$.

**Example 9.4.** Consider the set of integers $[0, 1, \dots, r-1]$. Let $p \ge r$ be prime and $h(k) = (ak+b) \pmod p$ where $a$ and $b$ are chosen randomly from $\{0, 1, \dots, p-1\}$.

## 9.2.4.5 Extensions

We have not discussed how to handle collisions. There are two main ways to handle collisions: chaining and open addressing.

- chaining: each slot in the hash table points to a linked list of all elements that hash to that slot.
- open addressing: when a collision occurs, we search for another empty slot in the hash table according to some probing sequence.

In chaining, all elements are stored in the hash table. In open addressing, each element is stored directly in the hash table. If a collision occurs, we probe for an empty slot.

The performance of these methods depends on the load factor $\alpha = n/m$, where $n$ is the number of elements and $m$ is the number of slots in the table. For chaining, the expected time for a search is $O(1+\alpha)$. For open addressing, the expected time for a search is $O(1/(1-\alpha))$, assuming $\alpha < 1$.

## 9.3 PRIORITY QUEUE

A priority queue is an abstract data type that supports operations on elements with priorities. The main operations are:

- insert(element, priority): add an element with a given priority to the queue.
- find-max(): return the element with the highest priority. own- delete-max(): remove the element with the highest priority.
- decrease-key(element, priority): decrease the priority of an element.

One way to implement a priority queue is using a heap. A heap is a complete binary tree that satisfies the heap property. For a max-heap, the key of each node is greater than or equal to the keys of its children. For a min-heap, the key of each node is less than or equal to the keys of its children.

The operations of a priority queue implemented with a heap can be performed in $O(\log n)$ time:

- insert: $O(\log n)$
- find-max: $O(1)$
- delete-max: $O(\log n)$
- decrease-key: $O(\log n)$

Binary trees are often represented using arrays. For a node at index $i$, its left child is at index $2i$, its right child is at index $2i+1$, and its parent is at index $\lfloor i/2 \rfloor$.

## 9.3.1 Heaps

The simplest implementation of a priority queue uses the data structure called a heap. A heap is a complete binary tree that at each node stores a member of the set and satisfies the properties

* every node has two children, except for the nodes in the lowest two levels of the tree,
* the lowest level of the tree is filled to right (see Figure 9.1) and
* the key value of every node is no greater than that of its children (known as the heap property).

Figure 9.1 shows an example of a heap with nodes having the integer keys 5, 6, 8, 12, 7, 9, 18, 15, 25, 13, 11 and 10.

Figure 9.1 A heap
