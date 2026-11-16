
and C to a stack, you can only remove them in the order C, B, A. You use the `push` (or `emplace`) function to add an element onto the stack and the `pop` function to remove an element from the stack. The `top` function accesses the element on the “top” of the stack. The following code shows `std::stack` in action:

Click here to view code image

```
#include <stack> to use std::stack

std::stack<int> myStack;

myStack.push(10);

myStack.push(20);

myStack.push(30);

for (int i = 0; i < 3; i++)
{

    std::cout << myStack.top() << ' ';

    myStack.pop();
}
```

Because of the LIFO behavior of a stack, the above code outputs the following:

```
30 20 10
```

As with queue, the major operations for `std::stack` all have constant time complexity.

## Maps

A **map** is an ordered collection of {key, value} pairs, sorted by key. Each key in the map must be unique. Because a map has both a key type and a value type, you must specify both types when declaring a map. The recommended way to add an element to a map is with the `emplace` function, which takes in the key and values as parameters. For example, the following code creates a `std::map` of months, where the key is the number of the month and the value is the string name of the month:

Click here to view code image

```
// #include <map> to use std::map

std::map<int, std::string> months;

months.emplace(1, "January");
months.emplace(2, "February");
months.emplace(3, "March");

// ...
```

The easiest way to access an element from a map is by using the `[]` operator and passing in the key. For example, the following would output `February`:

```
std::cout << months[2];
```

However, this syntax works as expected only if the key is in the map. To determine if a key is in a map, use the find function. This returns an iterator to the element, if found. (We discuss iterators in a moment.)

Internally, the std::map implementation uses a balanced binary search tree. This means that std::map can find an element by key in O(log n) (logarithmic) time. Insertion and removal from the map are also logarithmic. Furthermore, due to the binary search tree, looping over the contents of a map is in ascending order of the keys.

## Hash Maps

While a regular map maintains an ascending order of the keys, a hash map is unordered. In exchange for the lack of ordering, insertion, removal, and search are all O(1). Thus, in cases where you need a map but don't need ordering, a hash map yields better performance than a regular map.

The C++ hash map std::unordered_map has the same functions as std::map, just without any guaranteed ordering. To use the hash map class, use #include <unordered_map>.

## Iterators, Auto, and Range-Based For Loops

For looping over all the elements in a vector you can use the same syntax as for looping over an array. However, many of the other C++ STL collections, such as `list` and `map`, do not support this array syntax.

One way to loop over these other containers is with an **iterator**, which is an object that helps traverse the collection. Every C++ STL collection supports iterators. Each collection has a `begin` function that returns an iterator to the first element and an `end` function that returns an iterator to the last element. The type of the iterator is the type of the collection followed by `::iterator`. For example, the following code creates a list and then uses an iterator to loop over each element in the list:

Click here to view code image

```
std::list<int> numbers;

numbers.emplace_back(2);

numbers.emplace_back(4);

numbers.emplace_back(6);

for (std::list<int>::iterator iter = numbers.begin();
     iter != numbers.end();
     ++iter)
{
    std::cout << *iter << std::endl;
}
```

Note that the iterator is dereferenced with * , the same way a pointer is dereferenced. The syntax for looping over other collections with iterators is similar.

In the case of a map, the iterator actually points to a std::pair. So, given an iterator to an element in a map, you must use first and second to access the key and value, respectively. Returning to the months map from earlier, you can get an iterator to an element and output its data with the following code:

Click here to view code image

```
// Get an iterator to the element with the key 2
std::map<int, std::string> iter = months.find(2);

if (iter != months.end()) // This is only true if found
{
    std::cout << iter->first << std::endl; // Outputs
    std::cout << iter->second << std::endl; // Outputs
}
```

Typing out the long type names for iterators is annoying. C++11 provides the auto keyword to help reduce this pain. auto tells the compiler to deduce the type of a variable for you, based on the assigned value. For example, because the *begin* function returns an iterator of a very specific type, *auto* can deduce that correct type. There is no performance penalty for using *auto*, though some programmers find the code harder to understand.

Using *auto*, you can rewrite the list loop as follows:

Click here to view code image

```
// auto is deduced to be std::list<int>::iterator
for (auto iter = numbers.begin();
     iter != numbers.end();
     ++iter)
{
    std::cout << *iter << std::endl;
}
```

The code in this book uses *auto* only when it provides a benefit in readability.

Even with *auto*, the code for looping via iterators is clunky. Many other programming languages provide a foreach construct for looping over collections. C++11 has a similar construct called a **range-based for loop**. To loop over the numbers list with a range-based for loop, use the following syntax:

Click here to view code image

```
for (int i : numbers)
{
    // i stores the element for the current loop iteration
    std::cout << i << std::endl;
}
```

This loop makes a copy of each element in the list as it iterates over it. However, you can also pass by reference if you want to modify elements in the collection. Similarly, you can use const references.

You can also use auto for the type when writing a range-based for loop. However, as with using an explicit type, this makes a copy of each element. However, you can also use const and & with auto, if needed.

One disadvantage of a range-based for loop is that you can't add or remove elements in the collection during the loop. So, if you need this behavior, you must use another type of loop.

## ADDITIONAL READING

There are many excellent resources available online to help you learn and practice the fundamentals of C++. One such website is LearnCPP.com, which contains a very in-depth progression of topics. If you prefer traditional books, you should see Stephen Prata's book, which provides coverage of the basics. Eric Roberts's book covers both the fundamentals of C++ and relevant data structures.

Both of Scott Meyers's books are great resources for best practices in C++. They are short reads that provide many tips on how to achieve maximum effectiveness from C++ code.

There is also a great deal of information available on the C++ Standard Library. Bjarne Stroustrup, the creator of C++, devotes a large section of his book to the C++ collection implementations.

LearnCpp.com. Last modified April 28, 2016. http://www.learncpp.com.

Meyers, Scott. Effective C++, 3rd edition. Boston: Addison-Wesley, 2005.

Meyers, Scott. Effective Modern C++. Sebastopol: O'Reilly Media, 2014.

Prata, Stephen. C++ Primer Plus, 6th edition. Upper Saddle River: Addison-Wesley, 2012.

Roberts, Eric. Programming Abstractions in C++. Boston: Pearson, 2014.

Stroustrup, Bjarne. The C++ Programming Language, 4th edition. Upper Saddle River: Pearson, 2013.

## INDEX

### SYMBOLS

- * operator, 63

- + operator, 64

- = operator, 469

- == operator, 469

- - operator, 62

### NUMBERS

- 2D coordinate systems, 151

- 2D graphics, 14–15

- drawing, 19–21

- filtering analog sticks, 267–269

- implementing, 18–21

- Initialize function, 19

- scrolling backgrounds, 51–53

- Shutdown function, 19

- sprites, 42

- animating, 48–50

- drawing, 44–48

- 2D transformations
