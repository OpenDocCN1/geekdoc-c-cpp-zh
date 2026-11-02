Then you visit all pairs in that range:

```
cout << "Tom's friends: ";
for (auto pos = tom_range.first; pos != tom_range.second; pos++)
{
  cout << pos->second << ", ";
}
```

To erase an entry, call the erase member function with an iterator pointing to it:

```
friends.erase(tom_range.first); // Erases Tom's first friend
```

# EXAMPLE CODE

See special_topic_1 of your companion code for a program that demonstrates multiset and multimap.

![](bbox=[0.08, 0.43, 0.2, 0.52])

# WORKED EXAMPLE 15.1

# Word Frequency

Learn how to create a program that reads a text file and prints a list of all words in the file in alphabetical order, together with a count that indicates how often each word occurred in the file. See your E-Text or visit wiley.com/go/bc103.

![](bbox=[0.65, 0.43, 0.9, 0.57])

© Ermin Gutenberger/iStockphoto.

# 15.3 Implementing a Hash Table

In Section 15.1, you were introduced to the set data structure and its two implementations in the C++ standard library, hash tables and binary search trees. In these sections, you will see how hash tables are implemented and how efficient their operations are.

# 15.3.1 Hash Codes

The basic idea behind hashing is to place values into an array, at a location that can be determined from the value itself. Each value has a hash code, an integer value that is computed from a value in such a way that different values are likely to yield different hash codes.

Let us look at one way of computing a hash code for a string. We want to combine the char values of the string into an integer. We could simply add up all char values, but then permutations such as "eat" and "tea" would have the same hash code. A better way is to scramble the codes a bit:

```
int hash_code(const string& str)
{
  int h = 0;
  for (int i = 0; i < str.length(); i++)
  {
    h = 31 * h + str[i];
  }
  return h;
}
```