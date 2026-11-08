# Initialize

The initialization operations for array are:

+   - **Default constructor**  
+     When you define `array<int,4> x{}`, all elements are zero initialized. You can also initialize all—or some—elements according to the rules of aggregate initialization with `array<int,4>{1,2,3,4}` or `array<int,4>{1,2}`.
+   - **Copy constructor, move constructor**  
+     You can copy arrays of the same size and thus pass and return them by value. Moving is also possible if the element type allows it.

# Assignment

You have the following operations available to modify all content of an array at once:

+   - **Assignment operator**  
+     You can assign new values to an array by assigning it another array with a compatible element type and the same size. `operator=` is therefore defined as expected.
+   - **Assign**  
+     There is no assign because array also does not have a complete set of constructors.
+   - **Fill**  
+     However, there is `fill`, which allows you to set all values of an array at once, as you can see in [Listing 24.35].

# Insert and Delete

Inserting and deleting elements is not possible with array.

# Read and Write

You can read and write parts of an array in the following ways:

+   - **Index access**  
+     However, you can access the elements unprotected or protected with `[]` and at. You get back a reference that you can read and overwrite.
+   - **Iterators**  
+     The iterators of `array` are contiguous and random-access, meaning they can move forward, backward, and be arbitrarily positioned, similar to `vector`.
+   - **Beginning and end**  
+     You also have `front` and `back` available, which give you references to the first and last elements of the array, respectively.
+   - **Tuple interface**  
+     You can read and write an array like a tuple using `std::get<>`, as you can see in [Listing 24.36].