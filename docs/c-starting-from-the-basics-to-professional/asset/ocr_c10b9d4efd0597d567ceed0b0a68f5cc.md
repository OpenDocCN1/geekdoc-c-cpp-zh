```
~~~cpp
    std::cout << "The largest of numbers is " << largest(numbers) << std::endl;
    std::cout << "The largest of data is " << largest(data) << std::endl;
    std::cout << "The largest of names is " << largest(names) << std::endl;
}

// Finds the largest of an array of double values
double largest(const double data[], size_t count)
{
    double max{ data[0] };
    for (size_t i{ 1 }; i < count; ++i)
        if (max < data[i]) max = data[i];
    return max;
}

// Finds the largest of a vector of double values
double largest(const std::vector<double>& data)
{
    double max {data[0]};
    for (auto value : data)
        if (max < value) max = value;
    return max;
}

// Finds the largest of a vector of int values
int largest(const std::vector<int>& data)
{
    int max {data[0]};
    for (auto value : data)
        if (max < value) max = value;
    return max;
}

// Finds the largest of a vector of string objects
std::string largest(const std::vector<std::string>& words)
{
    std::string max_word {words[0]};
    for (const auto& word : words)
        if (max_word < word) max_word = word;
    return max_word;
}
~~~
```

This produces the following output:

```
~~~text
The largest of array is 44.6
The largest of numbers is 44
The largest of data is 8.7
The largest of names is Jane Austen
~~~
```