```
// all captured variables are copied
auto fun4 = [=]() mutable
{
    for (std::size_t i = 0; i < data.size(); ++i)
    { data[i] = 42.00; std::cout << data[i] << ","; }
    std::cout << '\n';
};
fun4();

// What has changed? No, we get the old ones i.e -99.99!
for (auto elem : data) { std::cout << elem << ","; }
```

Third, capture by using local variables in combination with a move is:

```
// Using local variable for capture
int size2 = 6; double val2 = 5.0;
std::vector<double> newData(size2, val2);

auto fun3 = [&localData = std::move(newData)]() mutable
{
    for (std::size_t i = 0; i < localData.size(); ++i)
    { localData[i] = 148.413; std::cout << localData[i] << ","; }
    std::cout << '\n';
};
fun3();
```

Finally, the solution using move semantics is:

```
// C++14 init capture
int sz = 5; double d = 1.414;
std::vector<double> arr(sz, d);
auto fun2 = [myData = std::move(arr)]() mutable
{
    std::cout << '\n';
    for (std::size_t i = 0; i < myData.size(); ++i)
    { myData[i] = 93.8344; std::cout << myData[i] << ","; }
    std::cout << '\n';
};
fun2();
```

It is instructive to run the code. For more complex cases, it might be an option to use function objects instead of lambda functions.

# 6.7.1 Living Without Generalised Lambda Capture

Generalised lambda capture is a C++14 feature. Before C++14 we had to depend on C++11 in combination with std::bind in order to emulate the feature. You may prefer