![](bbox=[0.111, 0.062, 0.734, 0.213])

![](bbox=[0.111, 0.283, 0.735, 0.365])

situation shown in figure 12.1, figure 12.3 shows what happens if element two is removed from our list. Again: only pointers need to be juggled. In this case it’s even simpler than adding an element: only two pointers need to be rerouted. To summarize the comparison between lists and vectors: it’s probably best to conclude that there is no clear-cut answer to the question what data structure to prefer. There are rules of thumb, which may be adhered to. But if worse comes to worst, a profiler may be required to find out what’s best.

The `list` container offers the following constructors, operators, and member functions:

+   - **Constructors:**
+     - A list may be constructed empty:
+   
+       As with the vector, it is an error to refer to an element of an empty list.
+     - A list may be initialized to a certain number of elements. By default, if the initialization value is not explicitly mentioned, the default value or default constructor for the actual data type is used. For example:
+     - A list may be initialized using a two iterators. To initialize a list with elements 5 until 10 (including the last one) of a `vector<string>` the following construction may be used:
+     - A list may be initialized using a copy constructor:
+   - The list does not offer specialized operators, apart from the standard operators for containers.

```
list<string> object;
```

```
list<string> object(5, string("Hello"));  // initialize to 5 Hello’s
list<string> container(10);                  // and to 10 empty strings
```

```
extern vector<string> container;
list<string> object(&container[5], &container[11]);
```

```
extern list<string> container;
list<string> object(container);
```