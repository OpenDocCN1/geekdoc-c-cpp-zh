If you have the choice of explicitly declaring iterators or STL functions to handle the internally, for example, by passing an rbegin() return value to a function, you should take the latter course. It's one less thing to do and one less opportunity to experience human fallibility.

The other iterators (back_insert_iterator, front_insert_iterator, and insert_iterator) also increase the generality of the STL algorithms. Many STL functions are like copy() in that they send their results to a location indicated by an output iterator. Recall that the following copies to a location at the beginning of dice::begin();

```
copy(casts, casts + 10, dice.begin());
```

These values overwrite the prior contents in dice, and the function assumes that dice has enough room to hold the values. That, copy() does not automatically adjust the size of the destination to fit the information sent to. Listing 16.10 takes care of that situation by declaring dice to have 10 elements, but suppose you don't know how big dice should be. Or you want to add elements to dice rather than overwrite ones.

The three insert iterators solve this problem by converting the copying process to an insertion process. Insertion adds new elements without overwriting existing data, and it uses automatic memory allocation to ensure the new information facts. A back_insert_iterator inserts items at the end of the container, and a front_insert_iterator inserts items from the front of the location specified as an argument to the insert_iterator constructor. All of these three iterators are the outputs of the container concept.

There are restrictions. A back_insert_iterator can be used only with container types that allow rapid insertion at the end. (Rapid refers to a constant time algorithm; the "Container Concepts", later in this chapter, discusses the time concept further). The vector class qualifies. A front_insert_iterator can be used only with container types that allow constant time insertion at the beginning. Here the vector class does not qualify, but the queue class does. The insert_iterator doesn't have these restrictions. Thus, you can use it to insert material at the front of a vector. However, a front_insert_iterator does so faster for the container types that supports it.

# Tip

You can use an insert_iterator to convert an algorithm that copies data into that one inserts data.

These iterators take the container type as a template argument and the actual container identifier as a constructor argument. This is, to create a back_insert_iterator for a vector<int> you called dice, you use:

```
back_insert_iterator<vector<int>> > back_iter(dice);
```

The reason you have to declare the container type is that the iterator has to make the appropriate container type. The code for the back_insert_iterator