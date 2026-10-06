# 500 C++ INTERLUDE 6 Iterators

We can call the for_each function to display all items in the collection as:

```
for_each(myList.begin(), myList.end(), displayOneItem);
```

With this one, C++ takes care of all the details. The compiler will insert code that begins at the first position of myList and sends each item to the function displayOneItem to be displayed until all items have been processed.

> Note: The syntax used to call most of the special functions that use iterators to process collections follows the form
> function_name(start_iterator, end_iterator, special_parameters);
> where special_parameters represents one or more parameters that the function needs to perform its task.

The function find. To search a collection for a target entry, you use the collection find. This function returns an iterator to the target if it exists in the collection. If the target is not in the collection, it returns an iterator to the list:

```
// Find the entry "Ace" in the collection myList
LinkedIterator<string> myCard = find(myList.begin(), myList.end(), "Ace");
```

The function count. Another useful function is count. This function returns the number of times a specified value occurs in the collection between the starting iterator and ending iterator:

```
// Count the number of occurrences of "Ace" in collection myList
int aceCount = count(myList.begin(), myList.end(), "Ace");
```

The function advance. To move an iterator forward a specific number of positions, you can use the advance function. It has a slightly different format:

```
advance(iterator, distanceToAdvance);
```

For example, if we needed to the fifth element of myList, we would use the following statements:

```
// Advance from first position to fifth (4 positions ahead)
LinkedIterator<string> myIterator = myList.begin();
advance(myIterator, 4);
```

The function distance. To determine how many entries remain to be processed, we can determine the distance from the current position to the end of the collection, using the function:

```
int numberRemaining = distance(myIterator, myList.end());
```

The function equal. To determine whether the elements in two lists are same, either for the entire list or for a subray within the lists, you can use the equal function. Suppose myList and yourList are two instances of LinkedList<string>. To determine if all entries in myList are equal to the first entries in yourList, you would write:

```
bool same = equal(myList.begin(), myList.end(), yourList.begin());
```