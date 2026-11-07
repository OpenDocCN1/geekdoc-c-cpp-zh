# Recipe 4: Using Associative Containers: Maps and Sets

# Situation

The "GitforGits" platform requires efficient data organization and access based on key-value associations or item uniqueness. In this context, the STL's associative containers become useful. Particularly important for these goals are set and map. Elements are stored as key-value pairs in a map, which enables quick retrieval using the unique key. In contrast, a set sorts elements automatically upon addition and guarantees that they are all unique. With these containers, our application may access data in an orderly and efficient manner, which significantly improves its performance and functionality.

# Practical Solution

Implementing map

A map is ideal for scenarios where you need to maintain a direct relationship between a key and a value, such as storing user settings or mapping user IDs to usernames.