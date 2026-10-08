+   21. How does a **multimap** differ from a **map**?
22. Why use a **copy()** algorithm when we could “just write a simple loop”?
23. What is a binary search?

# Terms

+   **accumulate()**
algorithm
application: ()
associative container
balanced tree
**binary_search()**
**copy()**
**copy_if()**
**equal_range()**
**find()**

+   **find_if()**
function object
generic
hash function
**inner_product()**
lambda
**lower_bound()**
**map**
predicate

+   searching
sequence
**set**
**sort()**
sorting
stream iterator
**unique_copy()**
**unordered_map**
**upper_bound()**

# Exercises

+   1. Go through the chapter and do all **Try this** exercises that you haven’t already done.
2. Find a reliable source of STL documentation and list every standard library algorithm.
3. Implement **count()** yourself. Test it.
4. Implement **count_if()** yourself. Test it.
5. What would we have to do if we couldn’t return **end()** to indicate “not found”? Redesign and re-implement **find()** and **count()** to take iterators to the first and last elements. Compare the results to the standard versions.
6. In the Fruit example in §21.6.5, we copy **Fruits** into the **set**. What if we didn’t want to copy the **Fruits**? We could have a **set<\*Fruit\*>** instead. However, to do that, we’d have to define a comparison operation for that set. Implement the Fruit example using a **set<\*Fruit\*>, \_Fruit_comparator\_**. Discuss the differences between the two implementations.
7. Write a binary search function for a **vector<int>** (without using the standard one). You can choose any interface you like. Test it. How confident are you that your binary search function is correct? Now write a binary search function for a **list<string>**. Test it. How much do the two binary search functions resemble each other? How much do you think they would have resembled each other if you had not known about the STL?
8. Take the word-frequency example from §21.6.1 and modify it to output its lines in order of frequency (rather than in lexicographical order). An example line would be: **3: C++** rather than **C++: 3**.