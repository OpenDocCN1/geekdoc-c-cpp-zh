
## CONSTANT MEMBER FUNCTIONS:

- s.capacity()       // Returns the maximum number of characters that could
                     // be put in s without having to add more memory.
- s.c_str()          // Returns a const array of characters that contains a null-
                     // terminated string with the same characters as s.
- s.data()           // Same as s.c_str() but without the null terminator.
- s.empty()          // Returns true if s has no characters.
- s.length()         // Returns the current number of characters in s
- s.max_size()       // Returns the maximum number of characters that s
                     // could ever have.
- s.size()           // Same as s.length().
- s1 == s2 and s1 != s2   // Boolean tests of whether two strings are equal or unequal.
- s1 < s2 and s1 > s2     // Tests for lexicographical orderings of strings.
- s1 <= s2 and s1 >= s2

## FUNCTIONS THAT GIVE ACCESS TO THE CHARACTERS OF THE STRING:

For an index in the range 0 to s.length() - 1, the notation s[index] or s.at(index) returns the character at the specified index. Both of these functions return a reference to a character. When the string is not const, then this reference can be used to change a character, such as s[2] = 'x'. The at version causes an exception when the index is out of range, but the s[index] behavior is undefined in this case.

## CONCATENATION:

The expression s1 + s2 is a new string containing the characters of s1 followed by those of s2.

## APPEND FUNCTIONS:

These add the specified characters to the end of what's already in the string, using one of the forms of arguments shown earlier.

- s.append(str) or s += str
- s.append(str, index, n)
- s.append(c) or s += c
- s.append(n, c)
- s.append(carry) or s += carry
- s.append(carry, n)
- s.append(begin, end)

## INSERT FUNCTIONS:

These insert new characters, specified using one of the forms of arguments shown earlier. These characters are inserted beginning at s[i]. The value of i must be less than or equal to s.size(). Any characters that were already at s[i] or beyond are shifted rightward to make room for the new characters.

- s.insert(i, str)
- s.insert(i, str, index, n)
- s.insert(i, n, c)
- s.insert(i, carry)
- s.insert(i, carry, n)

## REPLACE FUNCTIONS:

These functions replace len characters of s starting at s[i]. The value of i must be less than or equal to s.size(), and if there are fewer than len characters starting at this spot, then all characters to the end of the string are replaced. The new characters are specified using one of the forms of arguments shown earlier.

- s.replace(i, len, str)
- s.replace(i, len, str, index, n)
- s.replace(i, len, n, c)
- s.replace(i, len, carry)
- s.replace(i, len, carry, n)

## FUNCTIONS TO FIND A POSITION IN A STRING:

These functions return a value of type string::size_type. The return value is the constant string::npos if the character is not found.

- s.find(c) // Returns index of first occurrence of the character c in s
- s.find(c, i) // Returns index of first occurrence of c that is at or after s[i]
- s.rfind(c) // Returns index of final occurrence of the character c in s
- s.rfind(c, i) // Returns index of final occurrence of c that is at or before s[i]
- s.find(str) // Returns index of first occurrence of the substring str within s
- s.find(str, i) // Returns index of first occurrence of str that is at or after s[i]
- s.rfind(str) // Returns index of final occurrence of the substring str within s
- s.rfind(str, i) // Returns index of final occurrence of str that is at or before s[i]

## FUNCTIONS THAT RETURN A SUBSTRING:

- s.substr(i) // Returns a string containing characters from s[i] to the end of s
- s.substr(i, n) // Returns a string containing up to n characters, starting at s[i]

## OTHER MODIFICATION MEMBER FUNCTIONS:

- s.clear() // Removes all characters from s.
- s.erase() // Removes all characters from s.
- s.erase(i) // Removes all characters from s[i] to the end of s.
- s.erase(i, len) // Removes up to len characters starting at s[i].
- s.reserve(amount) // Requests that the capacity of s be changed to the specified amount (which may be smaller than the current capacity). However, the changed capacity will never be smaller than the current string size.
- s.resize(n, c) // Changes the length of s to n (if this increases the length, new characters are the character c).
- s.resize(n) // Same as s.resize(n, '\0').

## INPUT AND OUTPUT:

- cout << s // Print all of s to cout.
- cin >> s // Skip whitespace and then read characters into s until whitespace is encountered. The terminating whitespace is not read.
- getline(cin, s, c) // Read characters from cin into s until c is encountered. The terminating c is read but not added to the end of s.
- getline(cin, s) // Same as getline(cin, s, '\n')

## Vectors from <vector>, Lists from <list>, and Deques from <deque>

The vector<Item> template class provides a sequence of items, similar to the way that a string provides a sequence of characters. Although not required by the C++ Standard, the typical vector implementation stores the items in a dynamic array.

The list<Item> template class also provides a sequence of items, similar to our sequence class in Chapters 3 through 5. Insertions and deletions at any point that is marked by an iterator are more efficient with lists because they are typically implemented with a linked list.

The deque<Item> template class is a double-ended queue, which is a sequence with quick access to elements at both ends (as described in Section 8.4).

## CONSTRUCTORS AND ASSIGNMENT:

All three classes have a default constructor (creates an empty sequence), a copy constructor, and an assignment operator. The function w.assign(n, element) changes w to a sequence that contains n copies of the specified element.

## CONSTANT MEMBER FUNCTIONS:

```
w.capacity() // (Vector only) Returns the maximum number of items
that could be put in w without adding more memory.
w.empty() // Returns true if w has no items.
w.size() // Returns the current number of items in w.
w.max_size() // Returns the maximum number of elements that w could
ever have.
w1 == w2 and w1 != w2 // Boolean tests of whether two sequences are equal or unequal.
w1 < w2 and w1 > w2 // Tests for lexicographical ordering of sequences.
w1 <= w2 and w1 >= w2
```

## FUNCTIONS THAT GIVE RANDOM ACCESS TO THE ITEMS OF THE VECTOR (BUT NOT A LIST OR DEQUE):

For an index in the range of 0 to v.size() - 1, the notation v[index] or v.at(index) returns the item at the specified index. Both of these functions return a reference to the item. When the vector is not const, then this reference can be used to change an item such as v[2] = 'x';. The at version causes an exception when the index is out of range, but the v[index] behavior is undefined in this case.

## INSERT FUNCTIONS:

Each insert function has a parameter pos that is an iterator for the sequence. The new element is inserted at this position. Any items that were already at or beyond this position are shifted rightward to make room for the new items.

```
w.insert(pos, element) // Inserts new element at specified position.
w.insert(pos, n, element) // Inserts n copies of new element at specified position.
w.insert(pos, begin, end) // Inserts elements [begin..end) into the sequence at the
specified position.
```

## OTHER MODIFICATION MEMBER FUNCTIONS:

```
w.clear() // Removes all elements from w.
w.erase(pos) // Pos is an iterator for the sequence; this function removes the item
// at this position.
w.erase(begin, end) // Removes all elements from begin up to (but not including) *end,
// i.e., the left-inclusive interval [begin...end).
w.erase(i, len) // (Vector only) Removes up to len elements starting at w[i].
w.front() // Returns a reference to the first element of the sequence.
w.back() // Returns a reference to the last element of the sequence.
w.pop_back() // Removes the final element of w.
w.push_back(element) // Appends the specified element to the end of w.
w.pop_front() // Removes the first element of w.
w.push_front(element) // Inserts the specified element to the front of w.
w.reserve(amount) // (Vector only) Requests that the capacity of w be increased to the
// amount. (Unlike the string, this will never reduce the capacity.)
w.resize(n, element) // Changes the length of w to n (if this increases the
// length, new items are the specified element).
w.resize(n) // Changes the length of w to n (if this increases the length, new
// items are the default value of the Item type).
```

## FUNCTIONS THAT RETURN ITERATORS:

```
w.begin() // Returns an iterator that is positioned at the start of w.
w.end() // Returns an end iterator (just beyond the last item of w).
w.rbegin() // Returns a reverse iterator that is positioned at the last item of w.
w.rend() // Returns a reverse end iterator (just before the first item of w).
```

## Maps and Multimaps from <map>

The map<Key, Item> and multimap<Key, Item> template classes from <map> allow a programmer to store a collection of items in which each item has an associated key, similar to the hash tables of Chapter 12 (but stored in a different manner that depends on the keys being ordered by a less-than operator). The map is limited to having at most one distinct item for any given key, whereas the multimap allows many different items with the same key. The map and multimap have a variety of the member functions similar to the set, but they also allow unique map operations, described here:

## INSERTING AN ITEM WITH A PARTICULAR KEY.

To insert an item e with a key into a map m, write m[k] = e;. For a multimap, the syntax is more complex: m.insert(multimap<xxx,yyy>::value_type(k,e));, where xxx is the type of the key and yyy is the type of the items.

## RETRIEVING AN ITEM WITH A PARTICULAR KEY:

The item associated with key k can be retrieved from a map with the m[k] notation, for example: cout << m[k];. For a multimap, the sequence of items that all have a specified key k can be obtained in several ways. One approach used by Lippmann and Lajoie is to use the count and find functions, as shown here (where it is an iterator for the multimap m):

```
int i = m.count(k);
it = m.find(k);
for (i = 0; i < many; ++i, ++it)
// Do something with *it
```
