![](bbox=[0.1, 0.11, 0.6, 0.23])

The important thing here is what happens next: We insert a fourth element with push_back(), which has the following consequences:

+   Because the vector needs more memory internally, it allocates the new memory (for say, six elements), moves in the fourth string (we create a temporary Person and move it into the vector with push_back()), but also copies the existing elements to the new memory:

![](bbox=[0.12, 0.34, 0.62, 0.47])

+   At the end of this operation the vector destroys the old elements, releases the old memory for theses elements, and updates its members:

![](bbox=[0.12, 0.54, 0.62, 0.67])

The question is, why does the vector not use the move constructor to move the elements from the old to the new memory?

# Strong Exception Safety Guarantee

The reason that vector reallocation does not use move semantics is the strong exception handling guarantee we give for push_back(): When an exception is thrown in the middle of the reallocation of the vector the C++ standard library guarantees to roll back the vector to its previous state. That is, push_back() gives a kind of a transactional guarantee: either it succeeds or it has no effect.

The C++ standard was able to give this guarantee in C++98 and C++03 because there C++ could only copy the elements. If something goes wrong while copying the elements, the source objects are still available. Internal code that handles the exception simply destroys the copies created so far and release the new