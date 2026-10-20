t here is only one big caveat when using uniform initialization: a list constructor is always called before any other constructor. the canonical example comes from the stL vector class, which has an initializer list constructor and a separate constructor accepting an integer to define the vector’s size. Because initializer list constructors are called before any other constructor if curly braces are used, there are the following different behaviors:

```
vector<int> v(3); // vector, size 3, all elements initialized to 0
vector<int> v{3}; // vector with 1 element initialized to 3
```

Fortunately, the above situation does not arise often. however, when it does, you must understand the difference between uniform initialization and function style initialization.

F rom a design perspective, the main advantage of uniform initialization is that user defined types may be designed to accept lists of identically typed values for construction. therefore, containers, such as vectors, may be statically