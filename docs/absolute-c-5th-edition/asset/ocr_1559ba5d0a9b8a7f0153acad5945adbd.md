# Reverse Iterators

Sometimes you want to cycle through the elements in a container in reverse order. If you have a container with bidirectional iterators, you might be tempted to try the following:

```
vector<int>::iterator p;
for (p = container.end(); p != container.begin() ; --p)
    cout << *p << " ";
```

This code will compile, and you may be able to get something like this to work on systems, but container.end() is not a regular iterator but a sentinel, container.begin() is not a sentinel.

Fortunately, there is an easy way to do what you want. For a container with bidirectional iterators, there is a way to reverse everything using a kind of iterator known as a reverse iterator. The following code will work like:

```
vector<int>::reverse_iterator rp;
for (rp = container.rbegin(); rp != container.rend(); ++rp)
    cout << *rp << " ";
```

The member function rbegin() returns an iterator located at the last element. The member function rend() returns a sentinel that marks the "end" of the elements in the reverse order. Note that for an iterator of type reverse_iterator, the increment operator, ++ and -- work backwards towards the elements. In other words, the meanings of -- and ++ are interchangeable. The program in 19.3 demonstrates a reverse iterator.

reverse_iterator type also has a constant version, which is named const_reverse_iterator.

| Reverse Iterators |
| A reverse iterator can be used to cycle through all elements of a container with bidirectional iterators. The elements are visited in reverse order. The general scheme is as follows: |
| STL_container<datatype>::reverse_iterator rp;
for (rp = c.rbegin(); rp != c.rend(); ++rp)
Process_At_Location p; |

The object c is a class with bidirectional iterators.
When using reverse_iterator, you need to have some sort of declaration or something equivalent. For example, if c is a vector<int>, the following will suffice:

```
vector<int>::reverse_iterator rp;
```