```
```cpp
// class SumSquaresClass defines overloaded operator()
// that returns the sum of its first argument total
// and the square of its second argument value
class SumSquaresClass {
public:
    // add square of value to total and return result
    int operator()(int total, int value) {
        return total + value * value;
    }
};
```
```

# Calling Algorithm accumulate

We call accumulate three times:

+   - Lines 36–37 call **accumulate** with a pointer to sumSquares as its last argument.
+   - Lines 44–45 call **accumulate** with a **SumSquaresClass** function object as the last argument. **SumSquaresClass{}** in line 45 creates a temporary **SumSquaresClass** object and calls its constructor. That function object is then passed to **accumulate**, which calls the **SumSquaresClass** object's **operator()** function.
+   - Lines 50–51 call **accumulate** with an equivalent lambda. The lambda performs the same tasks as the function **sumSquares** and the overloaded **operator()** function in **SumSquaresClass**.

```
```cpp
int main() {
    std::array integers{1, 2, 3, 4};
    std::ostream_iterator<int> output{std::cout, " "};

    std::cout << "array integers contains: ";
    std::ranges::copy(integers, output);

    // calculate sum of squares of elements of array integers
    // using binary function sumSquares
    int result{std::accumulate(integers.cbegin(), integers.cend(),
        0, sumSquares)};

    std::cout << "\n\nSum of squares\n"
        << "via binary function sumSquares: " << result;

    // calculate sum of squares of elements of array integers
    // using binary function object
    result = std::accumulate(integers.cbegin(), integers.cend(),
        0, SumSquaresClass{});

    std::cout << "\n\nvia a SumSquaresClass function object: " << result;

    // calculate sum of squares array
    result = std::accumulate(integers.cbegin(), integers.cend(),
        0, [](auto total, auto value){return total + value * value;});

    std::cout << "\n\nvia a lambda: " << result << "\n";
}
```
```