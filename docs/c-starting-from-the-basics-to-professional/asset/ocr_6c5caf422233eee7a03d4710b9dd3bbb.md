The opposite of insert() is called erase(). The following sequence of statements removes, one by one, the same elements we added earlier using insert():

```
```
numbers.erase(numbers.end() - 3, numbers.end());    // Erase last 3 elements
numbers.erase(numbers.begin() + numbers.size() / 2); // Erase the middle element
numbers.erase(numbers.begin());                      // Erase the first element
printVector(numbers);    // 2 4 5
```
```

The overload of erase() with two parameters deletes a range of elements; the one with a single parameter deletes only a single element (remember this distinction; it'll be important again later in this chapter).

The complete source for the example we used throughout this section can be found in Ex20_09.

> > **Note** Most containers offer similar insert() and erase() functions (the only exception is std::array<>). Naturally, set and map containers will not allow you to indicate where to insert() an element (only sequence containers do), but they do allow you to erase() elements that correspond to either an iterator or iterator range. Consult your Standard Library reference for more details.

# ## Altering Containers During Iteration

In past sections we showed you how to iterate over elements in a container as well as how to insert() and erase() elements. The logical next question is then, what if you insert() or erase() elements while you are iterating over a container?

Unless otherwise specified (consult a Standard Library reference for details), any modification to a container is said to invalidate all iterators that were ever created for that container. Any further use of an invalidated iterator results in undefined behavior, which of course translates to anything from unpredictable results to crashes. Consider the following function template (recall from Chapter 10 that the use of the auto& placeholder as a parameter type makes this an abbreviated function template definition):

```
```
void removeEvenNumbers(auto& numbers)
{
    auto from{ numbers.begin() }, to{ numbers.end() };
    for (auto iter {from}; iter != to; ++iter)        /* Wrong! */
    {
        if (*iter % 2 == 0)
            numbers.erase(iter);
    }
}
```
```

The intent is to write a template that removes all even numbers from containers of a variety of types—be it vector<int>, deque<unsigned>, list<long>, set<short>, or unordered_set<unsigned>.

The problem is that this template contains two serious yet fairly realistic bugs, both triggered by the erase() in the loop's body. Once you modify a sequence (for instance through erase()) you should generally stop using any existing iterators. Yet the loop in removeEvenNumbers() ignores that. Instead, it simply soldiers on using both the to and iter iterators, even after invoking erase() on the container to which both these iterators refer. There's therefore no telling what will happen should you execute this code, but it most certainly will not be what you might've hoped for.