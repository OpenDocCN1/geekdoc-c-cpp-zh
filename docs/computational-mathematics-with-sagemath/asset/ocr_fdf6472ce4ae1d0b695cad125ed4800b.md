adjacent (incompatible) if their difference is a square. We will use for that the Subsets class which allows us here to iterate over all size-2 subsets.

```
```python
sage: n = 100; V = range(n+1)
sage: G = Graph()
sage: G.add_edges([
....:     (i,j) for i,j in Subsets(V,2) if is_square(abs(i-j)) ])
```
```

Since we are looking for a maximal number of “compatible” elements, we might call the independent_set method, which returns a maximal subset of non-adjacent elements.

```
```python
sage: G.independent_set()
[4, 6, 9, 11, 16, 21, 23, 26, 28, 33, 38, 43, 50,
56, 61, 71, 76, 78, 83, 88, 93, 95, 98, 100]
```
```

The answer is thus 24, and not “42” As a consequence, the quiz from “Le Monde 2” was not “the ultimate question of life, the universe, and everything”, whose answer should be searched elsewhere.

# ### 16.4.2   Task Assignment

We now face the following situation: for an important construction site, ten workers must complete a total of ten tasks. We can associate to each worker a list of tasks they are able to complete. How to distribute the tasks in an optimal way?

Here again, we start by translating the problem into a graph: it will be bipartite, defined on the union {w0,...,w9} ∪ {t0,...,t9} of workers and tasks, and we will define t_i as adjacent to w_j when w_j is able to complete task t_i.

```
```python
sage: tasks = {0: [2, 5, 3, 7], 1: [0, 1, 4],
....:          2: [5, 0, 4],        3: [0, 1],
....:          4: [8],              5: [2],
....:          6: [8, 9, 7],        7: [5, 8, 7],
....:          8: [2, 5, 3, 6, 4],  9: [2, 5, 8, 6, 1]}
sage: G = Graph()
sage: for i in tasks:
....:     G.add_edges(("w" + str(i), "t" + str(j) for j in tasks[i]))
```
```

It now only remains to use the matching method, which will return a maximal set of tasks that can be performed simultaneously by different people:

```
```python
sage: for task, worker, _ in sorted(G.matching()):
....:     print("{} can be performed by {}".format(task, worker))
t0 can be performed by w2
t1 can be performed by w3
t2 can be performed by w5
t3 can be performed by w8
t4 can be performed by w1
t5 can be performed by w7
t6 can be performed by w9
```
```