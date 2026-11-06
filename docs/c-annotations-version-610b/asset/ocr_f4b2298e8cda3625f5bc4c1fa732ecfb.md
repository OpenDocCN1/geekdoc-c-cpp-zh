```
MyClass copy constructor
MyClass destructor
pairs constructed
MyClass copy constructor
MyClass destructor
mapsm constructed
MyClass destructor
MyClass destructor
*/
```

When tracing the output of this program, we see that, first, the constructor of a MyClass object is called to initialize the anonymous element of the array pairs. This object is then copied into the first element of the array pairs by the copy constructor. Next, the original element is not required anymore and is destroyed. At that point the array pairs has been constructed. Thereupon, the map constructs a temporary pair object, which is used to construct the map element. Having constructed the map element, the temporary pair object is destroyed. Eventually, when the program terminates, the pair element stored in the map is destroyed too.

+   - A map may be initialized using a copy constructor:

```
extern map<string, int> container;
map<string, int> object(container);
```

# 12.3.6.2  The ‘map’ operators

The map supports, in addition to the standard operators for containers, the index operator.

The index operator may be used to retrieve or reassign individual elements of the map. The argument of the index operator is called a key.

If the provided key is not available in the map, a new data element is automatically added to the map using the default value or default constructor to initialize the value part of the new element. This default value is returned if the index operator is used as an rval.

When initializing a new or reassigning another element of the map, the type of the right-hand side of the assignment operator must be equal to (or promotable to) the type of the map’s value part. E.g., to add or change the value of element "two" in a map, the following statement can be used:

```
mapsm["two"] = MyClass();
```

# 12.3.6.3  The ‘map’ public members

The following member functions are available for the map container:

+   - `map::iterator begin();`
+   
+     this member returns an iterator pointing to the first element of the map.
+   
+   - `void clear();`
+   
+     this member erases all elements from the map.
+   
+   - `size_t count(key);`
+   
+     this member returns 1 if the provided key is available in the map, otherwise 0 is returned.
+   
+   - `bool empty();`
+   
+     this member returns true if the map contains no elements.