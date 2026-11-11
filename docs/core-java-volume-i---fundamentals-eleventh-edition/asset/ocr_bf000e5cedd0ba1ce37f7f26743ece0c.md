+   **`java.util.Stack<E>`** 1.0
+   
+   - `E push(E item)`  
+     pushes *item* onto the stack and returns *item*.
+   - `E pop()`  
+     pops and returns the top item of the stack. Don't call this method if the stack is empty.
+   - `E peek()`  
+     returns the top of the stack without popping it. Don't call this method if the stack is empty.

# ### 9.7.5 Bit Sets

The Java platform's `BitSet` class stores a sequence of bits. (It is not a *set* in the mathematical sense—*bit vector* or *bit array* would have been more appropriate terms.) Use a bit set if you need to store a sequence of bits (for example, flags) efficiently. A bit set packs the bits into bytes, so it is far more efficient to use a bit set than an `ArrayList` of `Boolean` objects.

The `BitSet` class gives you a convenient interface for reading, setting, and resetting individual bits. Using this interface avoids the masking and other bit-fiddling operations that are necessary if you store bits in `int` or `long` variables.

For example, for a `BitSet` named `bucketOfBits`,

```
```java
bucketOfBits.get(i)
```
```

returns `true` if the *i*th bit is on, and `false` otherwise. Similarly,

```
```java
bucketOfBits.set(i)
```
```

turns the *i*th bit on. Finally,

```
```java
bucketOfBits.clear(i)
```
```

turns the *i*th bit off.

> **C++ NOTE:** The C++ `bitset` template has the same functionality as the Java platform `BitSet`.