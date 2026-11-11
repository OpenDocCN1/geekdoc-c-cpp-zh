+   - `Random()`  
+     constructs a new random number generator.

# `java.util.random.RandomGenerator`

+   - `int nextInt(int n)`  
+     returns a random integer between 0 and n − 1.
+   
+   - `static RandomGenerator of(String name)`  
+     yields a random generator for the given algorithm name. The algorithm with name `L64X128MixRandom` is suitable for most applications.

# 4.6.8 Object Destruction and the `finalize` Method

Some object-oriented programming languages, notably C++, have explicit destructor methods for any cleanup code that may be needed when an object is no longer used. The most common activity in a destructor is reclaiming the memory set aside for objects. Since Java does automatic garbage collection, manual memory reclamation is not needed, so Java does not support destructors.

Of course, some objects utilize a resource other than memory, such as a file or a handle to another object that uses system resources. In this case, it is important that the resource be reclaimed and recycled when it is no longer needed.

If a resource needs to be closed as soon as you have finished using it, supply a close method that does the necessary cleanup. You can call the close method when you are done with the object. In Chapter 7, you will see how you can ensure that this method is called automatically.