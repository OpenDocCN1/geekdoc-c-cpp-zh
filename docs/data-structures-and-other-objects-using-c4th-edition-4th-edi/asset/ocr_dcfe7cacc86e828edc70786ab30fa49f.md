```
void add_vertex(const Item& label);
// Precondition: size( ) < MAXIMUM.
// Postcondition: The size of the graph has been increased by adding
// one new vertex. This new vertex has the specified label and no edges.
```

```
void add_edge(size_t source, size_t target);
// Precondition: (source < size( )) and (target < size( )).
// Postcondition: The graph has all the edges that it originally had, and
// also has another edge from the specified source to the specified target.
// (If this edge was already present, then the graph is unchanged.)
```

For example, the following four statements create the two-vertex graph shown in the picture. In this graph, vertex 0 ($v_0$) contains the `double` number 3.14, and vertex 1 ($v_1$) contains the `double` number 2.17:

![](bbox=[0.453, 0.391, 0.629, 0.442])

```
graph<double> t;
```

```
t.add_vertex(3.14); // Adds vertex 0, with data of 3.14
t.add_vertex(2.17); // Adds the next vertex, with data of 2.17
t.add_edge(1, 0); // Adds an edge from vertex 1 to vertex 0
```

As you can see from the example, the `add_vertex` member function of the graph class requires an argument, which is the label of the newly added vertex.

# Labeled Graph Class—Overloading the Subscript Operator

Once a graph is created, we want to access its vertex labels by using the usual “square bracket” notation from C++. For example, suppose that `g` is a 10-vertex labeled graph. To print the label of vertex 3, we would like to write this:

```
cout << g[3];
```

When used this way, the square brackets are called the **subscript operator**.

We also want the subscript operator to allow assignments and other changes to the labels. For example, suppose that `g`’s labels are integers. We want to be able to change the label of a vertex with a simple assignment statement such as this:

```
g[3] = 42; <- Change the label of vertex 3 to 42.
```

In C++, we can overload the subscript operator to behave in exactly this way. The overloading of the subscript operator is accomplished with the highlighted prototype in the following class definition: