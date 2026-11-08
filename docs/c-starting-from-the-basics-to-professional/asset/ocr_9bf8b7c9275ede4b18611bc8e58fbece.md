```
```cpp
// Output column headings
std::cout << std::format(table_format, "integer", "sum", "factorial");

unsigned int n {};
unsigned int sum {};
unsigned long long factorial {1ULL};

while (++n <= limit)
{
    sum += n;                         // Accumulate sum to current n
    factorial *= n;                   // Calculate n! for current n
    std::cout << std::format(table_format, n, sum, factorial);
}
```
```

The output from this program is the same as Ex5_04.cpp. The variables n, sum, and factorial are defined before the loop. Here the types of the variables can be different, so n and sum are defined as unsigned int. The maximum value that can be stored in factorial is limited, so this remains as type unsigned long long. Because of the way the calculation is implemented, the counter n is initialized to zero. The while loop condition increments n and then compares the new value with limit. The loop continues as long as the condition is true, so the loop executes with values of n from 1 up to limit. When n reaches limit+1, the loop ends. The statements within the loop body are the same as in Ex5_04.cpp.

> **Note**  Any for loop can be written as an equivalent while loop, and vice versa. For instance, a for loop has the following generic form:

```
```cpp
for (initialization; condition; iteration)
    body
```
```

This can typically be written using a while loop as follows:

```
```cpp
{
    initialization;
    while (condition)
    {
        body
        iteration;
    }
}
```
```

The while loop needs to be surrounded by an extra pair of curly braces to emulate the way the variables declared in the initialization code are scoped by the original for loop.