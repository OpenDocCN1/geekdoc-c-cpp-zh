+   - If the number is prime (line 101), line 102 displays a message. Otherwise, lines 105–110 display the non-prime number's prime factors and their counts.
+   - Finally, if the number is not prime, line 115 calls `proveFactors` to check whether the prime factors, when multiplied, reproduce the number.

```
```cpp
// show a task's FactorResults
void displayResults(const FactorResults& results) {
    // unpack results into name (std::string), number (long long),
    // isPrime (bool) and factors (std::map)
    const auto& [name, number, isPrime, factors] {results};

    std::cout << std::format("\n{} results:\n", name);

    // display whether value is prime
    if (isPrime) {
        std::cout << std::format("{} is prime\n", number);
    }
    else { // display prime factors
        std::cout << std::format("{}'s prime factors:\n", number);
        std::cout << std::format("{:<12}{:<8}\n", "Factor", "Count");

        for (const auto& [factor, count] : factors) {
            std::cout << std::format("{:<12}{:<8}\n", factor, count);
        }
    }

    // if not prime, prove that factors produce the original number
    if (!isPrime) {
        proveFactors(number, factors);
    }
}
```
```

# Creating and Executing a Task: Function template `std::async`

The `<future>` header (line 5) contains features that enable you to execute asynchronous tasks and receive the results of those tasks when they finish executing.

```
```cpp
int main() {
    std::cout << "\nMAIN LAUNCHING TASKS\n";
    auto future1{std::async(std::launch::async,
        getFactors, "Task 1", 1016669066116628993)}; // not prime
    auto future2{std::async(std::launch::async,
        getFactors, "Task 2", 1000000000000000003)}; // prime

    std::cout << "\nWAITING FOR TASK RESULTS\n";

    // wait for results from each task, then display the results
    displayResults(future1.get());
    displayResults(future2.get());

    std::cout << "\nMAIN ENDS\n";
}
```
```