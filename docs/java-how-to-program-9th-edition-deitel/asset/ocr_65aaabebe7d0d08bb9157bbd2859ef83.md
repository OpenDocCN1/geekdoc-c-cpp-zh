# Section 20.12 Properties Class

+   - A Properties object (p. 863) is a persistent subclass of Hashtable.
+   - The Properties no-argument constructor creates an empty Properties table. An overloaded constructor receives a Properties object containing default property values.
+   - Properties method setProperty (p. 863) specifies the value associated with its key argument. Method getProperty (p. 863) locates the value of the key specified as an argument. Method store (p. 865) saves the contents of a Properties object to specified OutputStream. Method load (p. 865) restores the contents of a Properties object from the specified InputStream.

# Section 20.13 Synchronized Collections

+   - Collections from the collections framework are unsynchronized. Synchronization wrappers (p. 866) are provided for collections that can be accessed by multiple threads simultaneously.

# Section 20.14 Unmodifiable Collections

+   - Unmodifiable collection wrappers (p. 866) throw UnsupportedOperationExceptions (p. 839) if attempts are made to modify the collection.

# Section 20.15 Abstract Implementations

+   - The collections framework provides various abstract implementations of collection interfaces from which you can quickly flesh out complete customized implementations.

# Self-Review Exercises

20.1 Fill in the blanks in each of the following statements:

+   a) A(n) ______ is used to iterate through a collection and can remove elements from the collection during the iteration.
+   b) An element in a List can be accessed by using the element's ______.
+   c) Assuming that myArray contains references to Double objects, ______ occurs when the statement "myArray[0] = 1.25;" executes.
+   d) Java classes ______ and ______ provide the capabilities of arraylike data structures that can resize themselves dynamically.
+   e) If you do not specify a capacity increment, the system will ______ the size of the Vector each time additional capacity is needed.
+   f) You can use a(n) ______ to create a collection that offers only read-only access to others while allowing read/write access to yourself.
+   g) Assuming that myArray contains references to Double objects, ______ occurs when the statement "double number = myArray[0];" executes.
+   h) Collections algorithm ______ determines if two collections have elements in common.

20.2 Determine whether each statement is true or false. If false, explain why.

+   a) Values of primitive types may be stored directly in a collection.
+   b) A Set can contain duplicate values.
+   c) A Map can contain duplicate keys.
+   d) A LinkedList can contain duplicate values.
+   e) Collections is an interface.
+   f) Iterators can remove elements.
+   g) With hashing, as the load factor increases, the chance of collisions decreases.
+   h) A PriorityQueue permits null elements.

# Answers to Self-Review Exercises

20.1 a) Iterator. b) index. c) autoboxing. d) ArrayList, Vector. e) double. f) unmodifiable wrapper. g) auto-unboxing. h) disjoint.