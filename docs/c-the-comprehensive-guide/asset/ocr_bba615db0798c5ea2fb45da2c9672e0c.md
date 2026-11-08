Even if you have a perfect hash function, you also need to ensure that you do not receive “degenerated” data at runtime. Unfortunately, you rarely have full control over the exact data.

For these two reasons, I can only recommend that you always choose the ordered associative containers with their guaranteed runtime behavior as your first choice of data structure. Only if you need the last bit of performance and can react to unforeseen data should you choose an unordered variant.

# Fill Level and Reordering

With these containers, it can happen that the number of buckets needs to be adjusted when inserting. This is called the *load factor*, and it uses the `size()/bucket_count()` ratio. You can query the load factor with `load_factor()`. When it reaches the `max_load_factor()`, an automatic increase occurs. If an automatic increase occurs, a complete reordering of the elements takes place—a rehash. All iterators into the container lose their validity. The order of the elements relative to each other is almost certainly different after such a step than before.

Similar to vector, you can never be sure if iterators are still valid after an insertion. In addition, you can (also similar to vector) use a call to `reserve` to ensure that this does not happen up to a given limit. And you can pass a number to the constructor of these containers when creating them.

You could also change the `max_load_factor`, but you normally shouldn't. Initially, this is set to 1.0. Do you remember that you can pass the initial bucket count to the constructor? A `max_load_factor` of 1.0 means that a rehash occurs when the number of elements exceeds this value. With a `max_load_factor` of 0.5, this would happen at half that number.

# 24.8.3  Methods of Unordered Associative Containers

I am not always very precise or detailed with the function signatures here to save space and maintain clarity. If I don’t include the parentheses with method, there are usually multiple overloads:

+   - **Constructors—**`Cont()`, `Cont(Compare)`, `Cont({...})`, `Cont(It, It)`, `Cont(from_range, ...)`  
+     The default constructor `Cont()` creates an empty container. With a pair of iterators from another compatible container, you can copy its contents. You can specify an initializer list that your container should contain at the beginning. For an `unordered_map`, this means you need to specify nested `{...}`, as each element must initialize a pair with two parameters—for example, `unordered_map<int,string>{{2,"two"},{3,"three"}}`. Starting from C++23, there are also *from_range* constructors.