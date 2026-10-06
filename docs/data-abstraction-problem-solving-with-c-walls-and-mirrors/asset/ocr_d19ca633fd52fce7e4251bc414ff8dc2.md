```
{
public:
    SortedListA();
    SortedListA(const SortedListA::ItemType& sList);
    virtual ~SortedListA();

    void insertSorted(const ItemType& newEntry);
    bool removeSorted(const ItemType& anEntry);
    int getPosition(const ItemType& anEntry) const;

    // The inherited methods remove, clear, getEntry, isNotEmpty, and
    // getLength have the same specifications as given in ListInterface.
    //
    // The following methods must be overridden to disable their
    // effect on a sorted list:
    bool insert(int newPosition, const ItemType& newEntry);
    void setEntry(int position, const ItemType& newEntry)
    throw(PrecondViolatedExcep);
}; // end SortedListA
#include "SortedListA.cpp"
#endif
```

Method definitions. Let's examine the implementations of the sorted list methods. The default constructor and destructor are straightforward; the copy constructor invokes LinkedList's copy constructor by an initializer:

```
template<class ItemType>
SortedListA<ItemType>::SortedListA()
{
} // end default constructor
```

```
template<class ItemType>
SortedListA<ItemType>(const SortedListA<ItemType>& sList)
    : LinkedList<ItemType>(sList)
```

```
{
} // end copy constructor
```

```
template<class ItemType>
SortedListA<ItemType>::~SortedListA()
{
} // end destructor
```

The method insertSorted first getsPosition to get the position of the new entry, ignores the sign of this position, and uses the result and LinkedList's insert method to complete its task. Note that since we will override insert in SortedListA, we must be careful not to call that implementation, but to call the base implementation instead.

```
template<class ItemType>
void SortedListA<ItemType>::insertSorted(const ItemType& newEntry)
{
    int newPosition = fabs(getPosition(newEntry));
```