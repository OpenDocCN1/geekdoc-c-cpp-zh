+   The container also needs a definition for a second small class, usually called const_iterator (written as one word with an underscore between "const" and "iterator"). This is the same as an ordinary iterator, except its member functions must not change the container in any way. Our bag will use a const_node_iterator for its const_iterator.

+   The container needs a begin member function, which creates and returns an iterator that refers to the container's first item. For the bag, this iterator will be positioned at the head element of the linked list. Actually, we'll need two versions of the begin function: an ordinary version that returns a bag iterator, and a constant member function that returns a bag const_iterator.

+   The container needs two end member functions (one of which is a constant member function), which return an iterator (or a const_iterator), indicating a position that is beyond the end of the container.

# The Bag Iterator

For our bag, the begin and end functions are simple enough that they can go inside the bag's class definition, like this:

```
template <class Item>
class bag
{
public:
  // TYPEDEFS
  typedef node_iterator<Item> iterator;
  typedef const_node_iterator<Item> const_iterator;
  ...

  // FUNCTIONS TO PROVIDE ITERATORS
  iterator begin( )
  { return iterator(head_ptr); }
  const_iterator begin( ) const
  { return const_iterator(head_ptr); }
  iterator end( ) // Using the iterator's default constructor
  { return iterator( ); }
  const_iterator end( ) const // Using the default constructor
  { return const_iterator( ); }

private:
  node<Item> *head_ptr; // Head pointer for the list
  size_type many_nodes; // Number of nodes on the list
};
```