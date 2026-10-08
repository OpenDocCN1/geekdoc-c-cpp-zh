In §21.6.3, we return to the Dow Jones example and use this generalized **inner_product**() as part of a more elegant solution.

# # 21.6 Associative containers

After **vector**, the most useful standard library container is probably the **map**. A **map** is an ordered sequence of (key,value) pairs in which you can look up a value based on a key; for example, my_phone_book["Nicholas"] could be the phone number of Nicholas. The only potential competitor to **map** in a popularity contest is **unordered_map** (see §21.6.4), and that's a **map** optimized for keys that are strings. Data structures similar to **map** and **unordered_map** are known under many names, such as *associative arrays*, *hash tables*, and *red-black trees*. Popular and useful concepts always seem to have many names. In the standard library, we collectively call all such data structures *associative containers*.

The standard library provides eight associative containers:

**Associative containers**

| | |
|---|---|
| **map** | an ordered container of (key,value) pairs |
| **set** | an ordered container of keys |
| **unordered_map** | an unordered container of (key,value) pairs |
| **unordered_set** | an unordered container of keys |
| **multimap** | a **map** where a key can occur multiple times |
| **multiset** | a **set** where a key can occur multiple times |
| **unordered_multimap** | an **unordered_map** where a key can occur multiple times |
| **unordered_multiset** | an **unordered_set** where a key can occur multiple times |

These containers are found in **<map>**, **<set>**, **<unordered_map>**, and **<unordered_set>**.

# ## 21.6.1 map

Consider a conceptually simple task: make a list of the number of occurrences of words in a text. The obvious way of doing this is to keep a list of words we have seen together with the number of times we have seen each. When we read a new word, we see if we have already seen it; if we have, we increase its count by one; if not, we insert it in our list and give it the value 1. We could do that using a **list** or a **vector**, but then we would have to do a search for each word we read. That could be slow. A **map** stores its keys in a way that makes it easy to see if a key is present, thus making the searching part of our task trivial: