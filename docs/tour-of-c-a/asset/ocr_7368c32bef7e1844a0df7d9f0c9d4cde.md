```
task char_seq(char start)
{
    auto value = start;
    while (true) {
        cout << "value: " << value << "\n"; // communicate result
        co_yield 0;
        ++value;
    }
}
```