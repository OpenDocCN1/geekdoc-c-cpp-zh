variable for you, based on the assigned value. For example, because the *begin* function returns an iterator of a very specific type, *auto* can deduce that correct type. There is no performance penalty for using *auto*, though some programmers find the code harder to understand.

Using *auto*, you can rewrite the list loop as follows:

# Click here to view code image

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

# Click here to view code image