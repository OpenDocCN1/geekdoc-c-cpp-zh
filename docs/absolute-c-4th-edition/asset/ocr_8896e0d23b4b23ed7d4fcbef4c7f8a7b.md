# REVERSE ITERATORS

Sometimes you want to cycle through the elements in a container in reverse order. If you have a container with bidirectional iterators, you might be tempted to try the following:

```
iterator p;
for (p = container.end( ); p != container.begin( ); p--)
cout << *p << " ";
```

This code will compile, and you may be able to get something like this to work on some systems, but there is something fundamentally wrong with it: container.end( ) is not a regular iterator but only a sentinel, and container.begin( ) is not a sentinel.

Fortunately, there is an easy way to do what you want. For a container with bidirectional iterators, there is a way to reverse everything using a kind of iterator known as a reverse iterator. The following will work fine:

```
reverse_iterator rp;
for (rp = container.rbegin( ); rp != container.rend( ); rp++)
cout << *rp << " ";
```

The member function rbegin( ) returns an iterator located at the last element. The member function rend( ) returns a sentinel the marks the "end" of the elements in the reverse order. Note that for an iterator of type reverse_iterator, the increment operator, ++, moves backward through the elements. In other words, the meanings of -- and ++ are interchanged. The program in Display 19.3 demonstrates a reverse iterator.

reverse_iterator type also has a constant version, which is named const_reverse_iterator.

reverse iterator

rbegin( )

rend( )

# REVERSE ITERATORS

A reverse iterator can be used to cycle through all elements of a container with bidirectional iterators. The elements are visited in reverse order. The general scheme is as follows:

```
reverse_iterator rp;
for (rp = c.rbegin( ); rp != c.rend( ); rp++)
    Process_At_Location p;
```

The object c is a container class with bidirectional iterators.

When using reverse_iterator you need to have some sort of using declaration or something equivalent. For example, if c is a vector<int>, the following will suffice:

```
using std::vector<int>::reverse_iterator;
```