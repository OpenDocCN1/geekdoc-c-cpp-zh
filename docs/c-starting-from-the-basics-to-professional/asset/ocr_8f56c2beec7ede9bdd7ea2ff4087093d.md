# Operations on array<>s As a Whole

You can compare entire array<> containers using any of the comparison operators as long as the containers are of the same size and they store elements of the same type. Here's an example:

```
```cpp
std::array these {1.0, 2.0, 3.0, 4.0};    // Deduced type: std::array<double, 4>
std::array those {1.0, 2.0, 3.0, 4.0};
std::array them  {1.0, 1.0, 5.0, 5.0};

if (these == those)  std::cout << "these and those are equal." << std::endl;
if (these != them)    std::cout << "those and them are not equal." << std::endl;
if (these > them)     std::cout << "these are greater than them." << std::endl;
if (them < these)     std::cout << "them are less than those." << std::endl;
```
```

Containers are compared element by element. For a true result for ==, all pairs of corresponding elements must be equal. For inequality, at least one pair of corresponding elements must be different for a true result. For all the other comparisons, the first pair of elements that differ produces the result. This is essentially the way in which words in a dictionary are ordered, where the first pair of corresponding letters that differ in two words determines their order. All the comparisons in the code fragment are true, so all four messages will be output when this executes.

```
```cpp
double these[] {1.0, 2.0, 3.0, 4.0};    // Deduced type: double[4]
double those[] {1.0, 2.0, 3.0, 4.0};
double them[]  {1.0, 1.0, 5.0, 5.0};

if (these == those)  std::cout << "these and those are equal." << std::endl;
if (these != them)    std::cout << "those and them are not equal." << std::endl;
if (these > them)     std::cout << "these are greater than them." << std::endl;
if (them < these)     std::cout << "them are less than those." << std::endl;
```
```

This code still compiles (at least, it probably does: see the upcoming note). So that looks promising. However, running this on our test system now produces the following disappointing result:

```
```text
those and them are not equal.
```
```

While those and them are indeed not equal, we had hoped to see all four messages like before. You can try it for yourself by running Ex5_13.cpp. The results differ depending on which compiler you use, but it's unlikely that you'll see all four messages appear as desired. So what exactly is going on here? Why does comparing regular arrays not work as expected? You'll find out in the next chapter. (You see, it's not just comics and television shows that know how to employ a cliffhanger.) For now just remember that applying comparison operators to plain array names is not at all that useful.

> **Note**  Comparison of C-style array types using `<`, `>`, `==`, or `!=` is deprecated as of C++20. This means that for now compilers are advised to issue a warning if you write code such as that of our earlier example, and that at some point in the future such code will no longer be allowed at all.