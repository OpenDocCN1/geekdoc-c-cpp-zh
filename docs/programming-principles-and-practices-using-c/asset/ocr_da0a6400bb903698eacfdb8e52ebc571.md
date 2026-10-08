More **vector** use:

+   1. Read some floating-point values (at least 16 values) from a file into a **vector< double>** called **vd**.
2. Output **vd** to **cout**.
3. Make a vector **vi** of type **vector<int>** with the same number of elements as **vd**; copy the elements from **vd** into **vi**.
4. Output the pairs of (**vd[i],vi[i]**) to **cout**, one pair per line.
5. Output the sum of the elements of **vd**.
6. Output the difference between the sum of the elements of **vd** and the sum of the elements of **vi**.
7. There is a standard library algorithm called **reverse** that takes a sequence (pair of iterators) as arguments; reverse **vd**, and output **vd** to **cout**.
8. Compute the mean value of the elements in **vd**; output it.
9. Make a new **vector<double>** called **vd2** and copy all elements of **vd** with values lower than (less than) the mean into **vd2**.
10. Sort **vd**; output it again.

# ## Review

+   1. What are examples of useful STL algorithms?
2. What does **find()** do? Give at least five examples.
3. What does **count_if()** do?
4. What does **sort(b,e)** use as its sorting criterion?
5. How does an STL algorithm take a container as an input argument?
6. How does an STL algorithm take a container as an output argument?
7. How does an STL algorithm usually indicate “not found” or “failure”?
8. What is a function object?
9. In which ways does a function object differ from a function?
10. What is a predicate?
11. What does **accumulate()** do?
12. What does **inner_product()** do?
13. What is an associative container? Give at least three examples.
14. Is **list** an associative container? Why not?
15. What is the basic ordering property of binary tree?
16. What (roughly) does it mean for a tree to be balanced?
17. How much space per element does a **vector** take up?
18. How much space per element does a **vector** take up?
19. Why would anyone use an **unordered_map** when an (ordered) **map** is available?
20. How does a **set** differ from a **map**?