
Use the graphs in Figure 20-18 for Exercises 9 through 14.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1437_0.png)

**FIGURE 20-18** Graphs for Exercises 9 through 14

- 9. Find the adjacency matrix of the graph in Figure 20-18(a).
- 10. Draw the adjacency list of the graph in Figure 20-18(a).
- 11. List the nodes of the graph in Figure 20-18(a) in a depth first traversal.
- 12. List the nodes of the graph in Figure 20-18(a) in a breadth first traversal.
- 13. List the nodes of the graph in Figure 20-18(b) in a breadth first traversal.
- 14. List the nodes of the graph in Figure 20-18(b) in a depth first traversal.
- 15. Find the weight matrix of the graph in Figure 20-19.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1437_1.png)

**FIGURE 20-19** Graph for Exercise 15

- 16. Consider the graph in Figure 20-20. Find the shortest distance from node 0 to every other node in the graph.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1438_0.png)

**FIGURE 20-20** Graph for Exercise 16

- 17. Find a spanning tree in the graph in Figure 20-21.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1438_1.png)

**FIGURE 20-21** Graph for Exercise 17

- 18. Find a spanning tree in the graph in Figure 20-22.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1438_2.png)

**FIGURE 20-22** Graph for Exercise 18

- 19. Find the minimal spanning tree for the graph in Figure 20-23, using the algorithm given in this chapter.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1439_0.png)

**FIGURE 20-23** Graph for Exercise 19

## PROGRAMMING EXERCISES

- 1. Write a program that outputs the nodes of a graph in a depth first traversal.
- 2. Write a program that outputs the nodes of a graph in a breadth first traversal.
- 3. Write a program that outputs the shortest distance from a given node to every other node in the graph.
- 4. Write a program that outputs the minimal spanning tree for a given graph.
- 5. The algorithm to determine the minimal spanning tree given in this chapter is of the order O(n³). The following is an alternative to Prim’s algorithm that is of the order O(n²).

  **Input:** A connected weighted graph G = (V, E) of n vertices, numbered 0, 1, ..., n - 1; starting vertex s, with a weight matrix W.

  **Output:** The minimal spanning tree.

  ```cpp
  Prim2(G, W, n, s)
  Let T = (V, E), where E = ∅.
  for (j = 0; j < n; j++)
  {
      edgeWeights[j] = W(s, j);
      edges[j] = s;
      visited[j] = false;
  }
  edgeWeights[s] = 0;
  visited[s] = true;
  while (not all nodes are visited)
  {
      Choose the node that is not visited and has the smallest weight, and call it k.
      visited[k] = true;
      E = E ∪ { (k, edges[k]) }
      V = V ∪ { k }
      for each node j that is not visited
          if (W(k, j) < edgeWeights[j])
          {
              edgeWeights[j] = W(k, j);
              edges[j] = k;
          }
  }
  return T;
  ```

  Write a definition of the function `Prim2` to implement this algorithm, and also add this function to the class `msTreeType`. Furthermore, write a program to test this version of Prim's algorithm.

Chapter 13 introduced and examined templates in detail. With the help of class templates, we developed (and used) a generic code to process lists. For example, we used the class `listType` to process a list of integers and a list of strings. In Chapters 16 and 17, we studied the three most important data structures: linked lists, stacks, and queues. In these chapters, using class templates, we developed generic code to process linked lists. In addition, using the second principle of object-oriented programming (OOP), we developed generic code to process ordered lists. Furthermore, in Chapter 17, we used class templates to develop generic code to implement stacks and queues. Along the way, you saw that a template is a powerful tool that promotes code reuse.

ANSI/ISO Standard C++ is equipped with a Standard Template Library (STL). Among other things, the STL provides class templates to process lists (contiguous or linked), stacks, and queues. This chapter discusses many important features of the STL and shows how to use the tools provided by the STL in a program.

## Components of the STL

The main objective of a program is to manipulate data and generate results. Achieving this goal requires the ability to store data into computer memory, access a particular piece of data, and write algorithms to manipulate the data.

For example, if all data items are of the same type and we have some idea of the number of data items, we could use an array to store the data. We can then use an index to access a particular component of the array. Using a loop and the array index, we can step through the elements of the array. Algorithms, such as those for initializing the array, sorting, and searching, are used to manipulate the data stored in an array. On the other hand, if we do not want to be concerned about the size of the data, we can use a linked list to process it. If the data needs to be processed in a Last In First Out (LIFO) manner, we can use a stack. Similarly, if the data needs to be processed in a First In First Out (FIFO) manner, we can use a queue.

The STL is equipped with these features to effectively manipulate data. More formally, the STL has three main components:

- Containers
- Iterators
- Algorithms

Containers and iterators are class templates. Iterators are used to step through the elements of a container. Algorithms are used to manipulate data. The following sections discuss each of these components in detail.

## Container Types

Containers are used to manage objects of a given type. The STL containers are classified into three categories, as follows:

- Sequence containers (also called sequential containers)
- Associative containers
- Container adapters

### Sequence Containers

Every object in a sequence container has a specific position. The three predefined sequence containers are:

- vector
- deque
- list

Before discussing container types in general, let us first briefly describe the sequence container vector. We do so because vector containers are similar to arrays and thus can be processed like arrays. Also, with the help of vector containers, we can describe several properties that are common to all containers. In fact, all containers use the same names for the common operations. Of course, there are operations that are specific to a container, which will be discussed when describing a specific container.

### Sequence Container: vector

A vector container stores and manages its objects in a dynamic array. Because an array is a random access data structure, the elements of a vector can be accessed randomly. Item insertion in the middle or beginning of an array is time consuming, especially if the array is large. However, inserting an item at the end is quite fast.

The name of the class that implements the vector container is `vector`. (Recall that containers are class templates.) The name of the header file containing the class `vector` is `vector`. Thus, to use a vector container in a program, the program must include the following statement:

```cpp
#include <vector>
```

Furthermore, to define an object of type vector, we must specify the type of the object because the class `vector` is a class template. For example, the statement:

```cpp
vector<int> intList;
```

declares `intList` to be a vector and the component type to be `int`. Similarly, the statement:

```cpp
vector<string> stringList;
```

declares `stringList` to be a vector container and the component type to be `string`.

### Declaring Vector Objects

The class `vector` contains several constructors, including the default constructor. Therefore, a vector container can be declared and initialized several ways. Table 21-1 describes how a vector container of a specific type can be declared and initialized.

**TABLE 21-1** Various Ways to Declare and Initialize a Vector Container

| Statement | Effect |
|---|---|
| `vector<elemType> vecList;` | Creates the empty vector container vecList. (The default constructor is invoked.) |
| `vector<elemType> vecList(otherVecList);` | Creates the vector container vecList and initializes vecList to the elements of the vector otherVecList. vecList and otherVecList are of the same type. |
| `vector<elemType> vecList(size);` | Creates the vector container vecList of size size. vecList is initialized using the default constructor. |
| `vector<elemType> vecList(n, elem);` | Creates the vector container vecList of size n. vecList is initialized using n copies of the element elem. |
| `vector<elemType> vecList(beg, end);` | Creates the vector container vecList. vecList is initialized to the elements in the range [beg, end), that is, all the elements in the range beg...end - 1. Both beg and end are pointers, called iterators in STL terminology. (Later in this chapter, we explain how iterators are used.) |
