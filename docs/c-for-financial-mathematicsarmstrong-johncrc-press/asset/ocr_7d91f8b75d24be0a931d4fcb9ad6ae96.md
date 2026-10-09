So, to see if an element exists in the map, we compare the iterator returned by find with the iterator returned by end.

Although all our examples have used **map**, the code for an **unordered_map** would be identical.

# ## 18.9.1 How a map works

A **map** typically stores its data in a tree structure consisting of a number of nodes. Each node stores a key, a value, and a pointer to the nodes to the left and to the right. Where there is no adjacent node, a null pointer is used to indicate this. This is illustrated in Figure 18.4 where the black circles indicate the null pointers.

![](bbox=[0.1, 0.32, 0.9, 0.65])

**FIGURE 18.4:** A possible arrangement for the nodes in a map.

The **map** class ensures that at all times the key of a node is always greater than the key of the nodes on its left and less than the key of the nodes on its right.

This means that when we wish to search for the data associated with a given key, it is easy to quickly navigate up the tree, taking either a left branch or right branch according to whether the key of the node you are currently looking at is greater than or less than your key. Typically you would expect the depth of the tree to have a height of $O(\log_{2}(N))$ and so it should only take $O(\log_{2}(N))$ steps to lookup an element with a given key.

Inserting data and removing data is a little more tricky than searching for data. When you insert and remove nodes you need to make sure that the ordering property is preserved. You also want to make sure that you keep the depth of the tree of order $\log_{2}(N)$ at all times. There are standard algorithms