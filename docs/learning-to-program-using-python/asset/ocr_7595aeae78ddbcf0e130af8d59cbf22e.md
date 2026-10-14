# ## Chapter 8

# # Dictionaries

Next to lists, dictionaries are one of the most useful data types in Python. Python dictionaries are unordered collections of objects, matched to a keyword. Python lists, on the other hand, are ordered collections that use a numerical offset.

Because of their construction, dictionaries can replace many "typical" search algorithms and data structures found in C and related languages. For those coming from other languages, Python dictionaries are just like a hash table, where an object is mapped to a key name.

Dictionaries include the following properties:

+   1. Accessed by keyword, not an offset. Dictionaries are similar to associative arrays. Each item in the dictionary has a corresponding keyword; the keyword is used to “call” the item.
2. Stored objects are in a random order to provide faster lookup. When created, a dictionary stores items in any order it chooses. To get a value, simply supply the key. If you need to order the items within a dictionary, you have to do it yourself; there are no built-in methods for it.
3. Dictionaries are variable length, can hold objects of any type (including other dictionaries), and support deep nesting (multiple levels of items can be in a dictionary, such as a list within a dictionary within another dictionary).