```
```cpp
// such as a network connection or a database.
std::array<double, 6> quotes =
                         { 24.44, 24.65, 24.99, 23.76, 22.30, 25.89 };

// Send each quote to the target buffer.
std::for_each(begin(quotes), end(quotes), [&](double quote)
{
    send(_target, quote);

    // Pause before sending the next quote.
    concurrency::wait(20);
});
// Send a negative (sentinel) value to indicate the end of
// processing.
concurrency::send(_target, -1.0);

// Set the agent to the finished state.
done();
}
};
```
```

The consumer class is:

```
```cpp
class Consumer : public concurrency::agent
{
private:
    // The source buffer to read from.
    concurrency::ISource<double>& _source;
public:
    explicit Consumer(concurrency::ISource<double>& source)
        : _source(source){}

    void run()
    {
        // Read quotes from the source buffer until we receive
        // a negative value.
        double quote;

        // Poll to see if any new values have arrrived
        while ((quote = concurrency::receive(_source)) >= 0.0)
        {
            // Print the quote.
            std::cout.setf(std::ios::fixed);
            std::cout.precision(2);
            std::cout << "Current quote is " << quote << '\n';

            // Pause before reading the next quote.
            concurrency::wait(10);
        }
    }
}
```
```