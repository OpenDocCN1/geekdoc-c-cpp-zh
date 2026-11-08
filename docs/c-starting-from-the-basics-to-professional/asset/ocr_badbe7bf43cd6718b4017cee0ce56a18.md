```
```cpp
            9.0, 100.0, 121.0, 12.0
        };
```
```

```
```cpp
    const size_t count{std::size(samples)};             // Number of samples
    show_data(samples, count, "Original Values");       // Output original values
    normalize_range(samples, count);                    // Normalize the values
    show_data(samples, count, "Normalized Values", 12); // Output normalized values
}
```
```

```
```cpp
// Outputs an array of double values
void show_data(const double data[], size_t count,
               const std::string& title, size_t width, size_t perline)
{
    std::cout << title << std::endl;  // Display the title

    // Output the data values
    for (size_t i {}; i < count; ++i)
    {
        // Display a data item (uses a dynamic field width: see Chapter 7)
        std::cout << std::format("{:{}.6g}", data[i], width);
        if ((i + 1) % perline == 0)     // Newline after perline values
            std::cout << '\n';
    }
    std::cout << std::endl;
}
```
```

If you compile and run this example, complete with the definitions of largest(), smallest(), shift_range(), scale_range(), and normalize_range() shown earlier, you should get the following output:

```
```
Original Values
        11      23      13       4      57
        36     317      88       9     100
       121      12
Normalized Values
  0.0223642  0.0607029  0.028754      0  0.169329
   0.102236         1  0.268371  0.0159744  0.306709
   0.373802  0.0255591
```
```

The output demonstrates that the results are what was required. The last two statements in main() could be condensed into one by passing the address returned by normalize_range() as the first argument to show_data():

```
```cpp
show_data(normalize_range(samples, count), count, "Normalized Values", 12);
```
```

This is more concise but clearly not clearer.