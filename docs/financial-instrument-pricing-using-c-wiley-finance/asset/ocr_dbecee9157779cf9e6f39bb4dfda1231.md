In this section we focus on cases S3 and S4. To this end, an example of S3 is:

```
void CaptureLocalVariable()
{
    // C++14 init capture with local variables
    int x = 1'000; // This is a digit separator
    auto fun4 = [&r = x]()
    {
        r *= 2;
        std::cout << "\nr: " << r << '\n';
    };

    // Undefined r
    // std::cout << r << '\n';

    fun4(); // Prints the value 2000
}
```

In this case the lifetime of the local variable x is the scope of the lambda function itself.

We now take an example of a mutable lambda function which processes a vector that has already been initialised outside the scope of the lambda function and that is modified in the body of the function. We present four alternatives.

First, capture by reference is:

```
int size = 4; double val = 2.71;
std::vector<double> data(size, val);

// By reference capture mode
auto fun = [&data]() mutable
{
    std::cout << "Vector by reference, values being changed\n";
    for (std::size_t i = 0; i < data.size(); ++i)
    {
        data[i] = 3.14; std::cout << data[i] << ",";
    }

    std::cout << '\n';
};
fun();

// data still exists and has been modified
for (std::size_t i = 0; i < data.size(); ++i)
std::cout << data[i] << ";"; }
```

Second, capture by value is:

```
std::cout << "Capture by value:\n";
int size = 4; double val = -99.99;
std::vector<double> data(size, val);
```