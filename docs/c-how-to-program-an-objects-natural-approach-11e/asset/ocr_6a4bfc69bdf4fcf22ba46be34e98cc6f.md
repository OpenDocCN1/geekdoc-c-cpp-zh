```
```cpp
using namespace std;

int main() {
    unsigned int seed{0}; // stores the seed entered by the user

    cout << "Enter seed: ";
    cin >> seed;

    // set up random-number generation
    default_random_engine engine{seed}; // seed the engine
    uniform_int_distribution randomDie{1, 6};

    // display 10 random die rolls
    for (int counter{1}; counter <= 10; ++counter) {
        cout << randomDie(engine) << " ";
    }

    cout << '\n';
}
```
```

```
```text
Enter seed: 67
6 2 5 6 6 2 2 6 2 1
```
```

```
```text
Enter seed: 432
3 5 6 1 6 1 4 4 2 2
```
```

```
```text
Enter seed: 67
6 2 5 6 6 2 2 6 2 1
```
```

**Fig. 5.4**  Randomizing the die-rolling program. (Part 2 of 2.)

# 5.8.4 Seeding the Random-Number Generator with random_device

You’ll generally seed the random-number generator engine with a **random_device** object (from header `<random>`), as we’ll show in Fig. 5.5. A random_device produces evenly spread random integers, which cannot be predicted.¹² However, the random_device documentation indicates that for performance reasons, it’s typically used only to seed random-number generation engines.¹³ Also, **random_device might be predictable on some platforms.**¹⁴ So, check your compiler’s documentation before relying on this for secure applications.

+   12. “Nondeterministic Algorithm.” Wikipedia. Wikimedia Foundation. Accessed April 14, 2023. https://en.wikipedia.org/wiki/Nondeterministic_algorithm.
+   13. “std::random_device.” Accessed April 14, 2023. https://en.cppreference.com/w/cpp/numeric/random/random_device.
+   14. “std::random_device.” Accessed April 14, 2023. https://en.cppreference.com/w/cpp/numeric/random/random_device.