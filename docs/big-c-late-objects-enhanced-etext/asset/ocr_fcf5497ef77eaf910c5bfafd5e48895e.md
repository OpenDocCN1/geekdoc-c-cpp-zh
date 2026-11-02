You can read a score back with the same notation:

```
```cpp
cout << "Tom's score: " << scores["Tom"];
```
```

If the key is not present in the map, the [] operator automatically inserts the key and a default value. If you don't want that (for example, because you have a constant reference to a map), use the at member function instead:

```
```cpp
int toms_score = scores.at("Tom");
```
```

To find out whether a key is present in the map, use the find member function. It yields an iterator that points to the entry with the given key, or past the end of the container if the key is not present.

The iterator of a map<K, V> with key type K and value type V yields elements of type pair<K, V>. The pair class is a simple class defined in the <utility> header that stores a pair of values. It has two public (!) data members, first and second. Therefore, you have to go through this process to see if a key is present:

A map iterator yields key/value pairs. If the map is ordered, they are visited in increasing key order.

```
```cpp
unordered_map<string, double>::iterator pos = scores.find("Harry"); // Call find
if (pos == scores.end()) // Check if there was a match
{
    cout << "No match for Harry";
}
else
{
    cout << "Harry's score: " << (*pos).second;
    // pos points to a pair<string, double>
}
```
```

As with pointers, you can write pos->second instead of (*pos).second.

The following loop shows how you iterate over the contents of a map:

```
```cpp
unordered_map<string, double>::iterator pos;
for (pos = scores.begin(); pos != scores.end(); pos++)
{
    cout << "The score of " << pos->first << " is " << pos->second << endl;
}
```
```

To remove a key/value pair from a map, call the erase member function:

```
```cpp
scores.erase("Tom");
```
```

If the key is present, it is removed, together with its associated value. If you have an iterator that already points to the key/value pair that you want to remove, you can pass that to the erase member function:

```
```cpp
scores.erase(pos);
```
```

A simple example to illustrate the use of maps is a telephone database. The database associates names with telephone numbers. One member function inserts elements into the database. There are member functions to look up the number associated with a given name. The member function print_all produces a listing of all entries. Because we use an unordered_map, the program does not list the telephone records in alphabetical order. If an ordered traversal is important, use a map instead of an unordered_map.

```
```cpp
sec02/tele.cpp
1 #include <iostream>
2 #include <unordered_map>
3 #include <utility>
4 #include <string>
5 #include <vector>
```
```