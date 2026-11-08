
This pattern, however, while still useful at times, is clearly clumsy, verbose, and quite error-prone. Luckily, there is a better way. For Ex20_13, you could use the following two statements instead (see Ex20_13A):

```cpp
std::vector<int> odd_numbers;
std::copy_if(begin(numbers), end(numbers), back_inserter(odd_numbers),
             [](int n) { return n % 2 == 1; });
```

With this technique, there is no need to over-allocate and thus no need to `erase()` any redundant elements afterward either. Instead, you create a special “fake” iterator through the `std::back_inserter()` function. In our example, each element that `copy_if()` assigns through this special output iterator is effectively forwarded to the `push_back()` function of `odd_numbers`—the container you passed to `back_inserter()` when you created the iterator. The end result is therefore the same—all odd numbers are added to `odd_numbers`—but this time you did so with less code and, more importantly, code that is much clearer, and that leaves considerably less room for error.

> **Tip** The `<iterator>` module defines the `back_inserter()`, `front_inserter()`, and `inserter()` functions that create “fake” iterator objects that trigger, respectively, `push_back()`, `push_front()`, and `insert()` whenever a value is assigned to these iterators after dereferencing. Use these functions whenever an algorithm needs to output values into a container.

## The Remove-Erase Idiom

Often you need to delete all elements from a container that satisfy specific conditions. With the `removeEvenNumbers()` function of Ex20_10 earlier in this chapter, we showed you how you can do this using a rather complex `for` loop that iterates over all the elements of the container, checks whether an element satisfies the conditions, and if so calls `erase()` on the container to remove the element. Implementing it this way, however, can be both inefficient and error-prone. Take a `vector<>` as an example. If you remove an element from the middle of the `vector<>`, all subsequent elements need to be shifted down to fill the gap of the removed element. That is very inefficient (it exhibits quadratic complexity). Also, when removing elements from the container while you are iterating over that same container, you need to take extra care that the iterator is correctly handled, as discussed earlier. This is prone to errors. The remove-erase idiom, as well as the higher-level helper functions discussed in the next subsection, are therefore far more effective methods to remove elements from containers.

As the name suggests, the remove-erase idiom typically involves an invocation of a `remove()` or `remove_if()` algorithm, followed by an invocation of an `erase()` member function of a container.

> **Caution** Algorithms such as `remove()` and `remove_if()` do not actually remove any elements from a container. They can’t, because they only have access to iterators. Without access to the container or its member functions, algorithms cannot possibly `erase()` any elements. Instead, such algorithms operate by moving all elements that are to be kept to the front of the input range.

When you apply algorithms such as `remove()` and `remove_if()` to the full range of a sequence container, all elements that should be erased thus flock to the tail of the sequence. To this end, `remove()` and `remove_if()` return an iterator to the first element that should be erased. You generally use this iterator as a first argument to the `erase()` method of the container to erase any and all excess elements. First you `remove()`, then you `erase()`. Hence the name of the idiom: remove-erase.

Let’s see how the remove-erase idiom works with some actual code. You can use the same program as Ex20_10, only this time you replace the `removeEvenNumbers()` with this version:

```cpp
void removeEvenNumbers(std::vector<int>& numbers)
{
    // Use the remove_if() algorithm to remove all even numbers
    auto first_to_erase{ std::remove_if(begin(numbers), end(numbers),
                         [](int number) { return number % 2 == 0; }) };
    // Erase all elements including and following first_to_erase
    numbers.erase(first_to_erase, end(numbers));
}
```

The output of the resulting program (available in Ex20_14) should then remain the same:

```text
The original set of numbers: 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20
The numbers that were kept: 1 3 5 7 9 11 13 15 17 19
```

It may be instructive to see what happens if you remove the line that calls `numbers.erase()` from `removeEvenNumbers()`. If you do that, the output almost certainly becomes the following:

```text
The original set of numbers: 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20
The numbers that were kept: 1 3 5 7 9 11 13 15 17 19 11 12 13 14 15 16 17 18 19 20
```

As you can see, `remove_if()` simply moves all elements that are to be kept (odd numbers 1 till 19) to the front of the range, leaving the back of the range in disarray. That is, the algorithm does not go to the trouble of nicely moving all even numbers to the back of the range as well. Doing so would only be a waste of time: The back of the range is meant to be erased, so it’s okay if there’s odd numbers left there! Algorithms such as `remove()` and `remove_if()` are always meant to be followed by a call to `erase()`. Always. You can use `std::partition()` if you also want the even numbers to move to the back of the range.

> **Caution** Take care—and we cannot repeat this enough—not to forget the second argument to the call to `erase()`! It must be the end iterator of the container. If you forget this second argument, `erase()` will just erase the single element pointed to by the iterator passed as the first argument. In Ex20_14, for instance, only the number 11 would then be removed.

## Erase Functions

Compared to loops where you either increment an iterator or assign the result of `erase()` (as in the original `removeEvenNumbers()` function of Ex20_10), the algorithm-based remove-erase idiom is already a big step forward. But it still remains somewhat error-prone (it's ever so easy to forget the second argument of `erase()`), and it for sure remains rather wordy (two function invocations just to remove some elements?). C++20 therefore added nonmember function templates `std::erase(container, value)` and/or `std::erase_if(container, function)` to most container modules (all except `<array>`). Using `std::erase_if` you can, for instance, simplify `removeEvenNumbers()` from Ex20_14 as follows:

```cpp
void removeEvenNumbers(std::vector<int>& numbers)
{
    std::erase_if(numbers, [](int number) { return number % 2 == 0; });
}
```

Neat, right? The resulting program is available in Ex20_14A.

> **Tip** There are no `std::erase()` nonmember functions for sets or maps, only `std::erase_if()` functions. You should use the `erase()` member functions of these containers instead.

> **Note** It's not because `std::erase()` and `std::erase_if()` have been introduced that you no longer need to know the remove-erase idiom. Of course these functions should replace all applications of the idiom—that is, invocations of `remove()` or `remove_if()` followed by an invocation of `erase()`—but `remove()` and `remove_if()` are not the only algorithms for which this idiom is applicable. We refer you to Exercise 20-8 for an example.

## Sorting

Another key operation for arrays and sequence containers is sorting their elements. You may need this to present these elements to the user in a sorted order, but often also as a prerequisite for further algorithmic processing (such as with `std::binary_search()`, `std::merge()`, `std::set_intersection()`, and so on).

The `std::sort()` algorithm is defined in `<algorithm>` and sorts a range of elements. The first two arguments passed to the algorithm are the begin and end iterators of the range to sort. The third argument passed is an optional comparator. If no comparator is given, the elements are sorted in ascending sequence. That is, if applied to a range of strings, the strings will be sorted lexicographically. The following example sorts a range of strings twice, first lexicographically and then according to the length of each string:

```cpp
// Ex20_15.cpp - Sorting strings
import <iostream>;
import <string>;
import <vector>;
import <algorithm>;
```
