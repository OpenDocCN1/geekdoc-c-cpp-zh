# Programming Projects

24. The get_union template function requires that the containers keep their elements in sorted order to allow the function template to be implemented in a more efficient way.

# Programming Projects

Visit www.myprogramming.com to complete exercises online and get instant feedback.

+   1. The point of this exercise is to demonstrate that an object that behaves like an iterator is an iterator. More precisely, if an object accesses some container and behaves like an iterator of a particular strength, then that object can be used as an iterator to manipulate the container with any of the generic functions that require an iterator having strength. However, while the generic algorithms can be used with this container, the member functions, such as begin and end, (of course) will not be present (for example, in an array) unless they have been explicitly coded for that container. We will restrict this exercise to arrays of double, but the same message would hold true for any base type.
a. Argue from the properties of random-access iterators that a pointer points to an element of an array behaves exactly as a random-access iterator.
b. Argue further that
i) the name of the array is a pointer to point to the first element and so the array name can serve as a "begin" iterator and
ii) (the name+) + (the size of the array) can serve as an "end" pointer. (Of course, this points one past the end, as it should).
c. Write a short program in which you declare an array of double size 10, and populate array with 10 doubles. Then call the sort generic algorithm with these pointer values as arguments and display the results.

+   2. This problem intends to illustrate removal of several elements of a particular item from a container with the remove generic function. A side effect is to examine the behavior of the generic function that comes with your compiler. We have observed some variation in the behavior of remove from one compiler to another). Before you start, look up the behavior of the remove generic algorithm as described by your STL document or Web site. (For example, point your browser at http://www.sig.com/stl/remove.html. This worked as of the publication date).
a. Modify the array declaration in Programming Project 1.9 to include several elements with the same value (say, 4,0, but you can use any value for this exercise). Make sure that these are not all together. Using the modifying generic function remove (see Display 19.19) to remove all elements 4 (that is, the value you duplicated in the array). Test.
b. Use the array of double from part to build a list and a vector that have the same contents as the array. Do this using the container constructor that has two iterators as arguments. The vector and list classes each have a constructor that takes two iterators as arguments and initializes the vector or list to