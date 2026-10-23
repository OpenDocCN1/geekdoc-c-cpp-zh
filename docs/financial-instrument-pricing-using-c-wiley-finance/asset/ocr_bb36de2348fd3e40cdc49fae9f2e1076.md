```
// Modify the elements in the container
std::for_each(myList.begin(), myList.end(), [] (double& d)
    {d *= 2.0;});

// Print the elements of the container
std::for_each(myList.begin(), myList.end(), [] (double d)
    {std::cout << d << ", ";});

    return 0;
}
```

Here we see how lambda functions are applied to each element of the list. We can also rewrite the above code using free functions:

```
// Functions that operate on types
template <typename T>
    void Modify(T& t)
{
    t *= 2.0;
}

template <typename T>
    void Print (const T& t)
{
    std::cout << t << ", ";
}

int main()
{ // Using free functions

    std::list<double> myList;
    myList.push_back(1.0); myList.push_back(2.0);
    myList.push_back(3.0);myList.push_back(4.0);

    // Modify the elements in the container
    std::for_each(myList.begin(), myList.end(), Modify<double>);

    // Print the elements of the container
    std::for_each(myList.begin(), myList.end(),
        [] (double d) {std::cout <<d << ", ";});

                    return 0;
}
```

In both cases we see the basic principles underlying the functional programming paradigm. In particular, most STL algorithms are based on the general principle of iterating in a