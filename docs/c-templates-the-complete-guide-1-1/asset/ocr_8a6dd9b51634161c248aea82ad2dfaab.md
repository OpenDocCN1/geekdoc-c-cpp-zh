```
```cpp
}
ListModeIterator<T>* current = nullptr;
}
```
```

ListModeIterator provides all of the correct operations and nested types needed in a forward iterator, and requires very little code to implement them. Most of the hard work, defining member functions for all of the required operations, requires only a small amount of extra work.

# ## Hiding the interface

One drawback in our implementation of ListModeIterator is that we have to expose as public all of the operations that are used by the algorithms (operator*, operator++, operator==, and so on). To maintain this requirement, we can rework IteratorFacade to perform all of its operations in the derived class through a separate access class, which we call IteratorFacadeAccess:

Click here to view code image

```
```cpp
Iterator/IteratorFacadeChecked.hpp
```
```

```
```cpp
// "friend" this class to allow IteratorFacade access
// to the operations of IteratorFacadeAccess
class IteratorFacadeAccess
{
  // only IteratorFacade can use these definitions
  template<typename Derived, typename Value, typename
    Reference, typename Difference>
  friend class IteratorFacade;

  // required of all iterators
  template<typename Reference, typename Iterator>
  static Reference dereference(Iterator const& i) {
    return i.dereference();
  }

  // required of bidirectional iterators
  template<typename Iterator>
  static void decrement(Iterator& i) {
    return i.decrement();
  }

  // required of random-access iterators
  template<typename Iterator, typename Distance>
  static void advance(Iterator& i, Distance n) {
    return i.advance(n);
  }

  // ...
};
```
```

This class provides static member functions for each of the core iterator operations, calling the corresponding (static) member function of the provided iterator. All of the static member functions are private, with the access only granted to IteratorFacade itself. Therefore, our ListModeIterator can make IteratorFacadeAccess a friend and keep the interface nested in the facade:

Click here to view code image

```
```cpp
friend class IteratorFacadeAccess;
```
```

# ## Iterator Adaptors

Our IteratorFacade makes it easy to build an iterator adaptor that takes an existing iterator and modifies its behavior. This provides even more flexibility when faced with reusing an iterator over an transformed view of the underlying sequence. For example, we might have a container of Person objects:

Click here to view code image

```
```cpp
Iterator/iterator_adaptor.hpp
```
```