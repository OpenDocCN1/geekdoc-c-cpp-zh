more efficient implementation that we will examine in Chapter 10. But before we get to that implementation, let's examine some of the multiset member functions.

# Some Multiset Members

Constructors. A default constructor creates an empty multiset, a copy constructor makes a copy of another multiset. There are also other constructors that we won't use.

# Members that are similar to the bag.

These members are similar to our bag:

+   - A type definition for the value_type
+   - A type definition for the size_type
+   - size_type count(const value_type& target) const;
+   - size_type erase(const value_type& target);
+   - size_type size( ) const;

# The insert member function.

The multiset's insert function can be used exactly like the bag's insert function to add an item to a multiset. However, the actual prototype for the multiset's insert function specifies a return value called an iterator, as shown here:

```
iterator insert(const value_type& entry);
```

Let's examine the multiset's iterator in some detail.

# Iterators and the [...] Pattern

An iterator is an object that permits a programmer to easily step through all the items in a container, examining the items and (perhaps) changing them. Any STL container has a standard member function called begin that returns an iterator providing access to the first item in the container.

For a multiset, this "first" element is the smallest item according to the "less than" ordering that must be provided for the item type of any multiset. For other kinds of container classes, the "first" element might be implemented in some other way, and the exact mechanism used by begin isn't usually important.

The important concept is a general pattern whereby a programmer can use the begin function and related operations to step through all the items in a container. In all, there are four operations required for the pattern:

+   - begin: A container has a begin member function that we have already discussed. Its return value is an iterator that provides access to the first item in the container. For example, suppose that actors is a multiset of strings. Then we can write this code to obtain the beginning iterator:

```
multiset<string>::iterator role;
role = actors.begin( );
```