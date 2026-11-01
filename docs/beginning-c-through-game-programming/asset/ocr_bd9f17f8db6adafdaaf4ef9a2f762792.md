the same thing, but the STL containers offer more flexibility and power than a simple but trusty array. The STL defines a variety of container types; each works in a different way to meet different needs.

The algorithms defined in the STL work with its containers. The algorithms are common functions that game programmers find themselves repeatedly applying to groups of values. They include algorithms for sorting, searching, copying, merging, inserting, and removing container elements. The cool thing is that the same algorithm can work its magic on many different container types.

Iterators are objects that identify elements in containers and can be manipulated to move among elements. They're great for, well, iterating through containers. In addition, iterators are required by the STL algorithms.

All of this makes a lot more sense when you see an actual implementation of one of the container types, so that's up next.

# Using Vectors

The vector class defines one kind of container provided by the STL. It meets the general description of a dynamic array—an array that can grow and shrink in size as needed. In addition, vector defines member functions to manipulate vector elements. This means that the vector has all of the functionality of the array plus more.

At this point, you may be thinking to yourself: Why learn to use these fancy new vectors when I can already use arrays? Well, vectors have certain advantages over arrays, including:

+   - Vectors can grow as needed while arrays cannot. This means that if you use a vector to store objects for enemies in a game, the vector will grow to accommodate the number of enemies that get created. If you use an array, you have to create one that can store some maximum number of enemies. And if, during play, you need more room in the array than you thought, you're out of luck.
+   - Vectors can be used with the STL algorithms while arrays cannot. This means that by using vectors you get complex functionality like searching and sorting, built-in. If you use arrays, you have to write your own code to achieve this same functionality.