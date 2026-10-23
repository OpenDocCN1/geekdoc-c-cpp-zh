```
```cpp
void Shuffle()
{
    // IV. Shuffling
    std::cout << "\n**** Block IV, Shuffling ****\n";
    // Shuffle
    std::vector<int> vecR = { 1, 2, -2, 3, -3, 4, -4, 5, -5, 8, 9, 7 };

    std::random_shuffle(vecR.begin(), vecR.end());
    print(vecR, std::string("Modified, random shuffle: "));

    // C++11
    std::default_random_engine eng;
    std::shuffle(vecR.begin(), vecR.end(), eng);
    print(vecR, std::string("vecR after shuffle"));

    // Moving elements to the front
    std::vector<int> vecP = { 1, 2, 3, 4, 5, 6, 2, 7, 8, 9 };
    print(vecP, "vecP");
}
```
```

The output is:

```
```text
**** Block IV, Shuffling ****
Modified, random shuffle: 9, 2, 8, -2, 1, 7, 5, 3, -3, -4, -5, 4,
vecR after shuffle: 1, 9, -2, 2, -5, 3, 5, 4, -4, -3, 7, 8,
vecP: 1, 2, 3, 4, 5, 6, 2, 7, 8, 9,
```
```

These algorithms are useful when shuffling randomly generated numbers.

# 18.2.5 Creating Partitions

There are three algorithms in this category:

+   - Return the first position for which a unary predicate returns `false` (two functions).
+   - Partition a range into two subranges.

A code sample is:

```
```cpp
void RangePartition()
{
    // V. Partitioning a range
    std::cout << "\n**** Block V, Moving elements to front ****\n";
    std::vector<int> vecP = { 1, 2, 3, 4, 5, 6, 2, 7, 8, 9 };
    print(vecP, "vecP");

    // Partitioning: moving all the elements in a range to the front.
    // All elements greater than 6; relative order not preserved
    std::vector<int>::iterator posP = std::partition(vecP.begin(), vecP.end(),
```
```