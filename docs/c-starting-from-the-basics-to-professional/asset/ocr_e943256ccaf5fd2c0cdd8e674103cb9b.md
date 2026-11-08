+   - `search()` / `find_end()` search for a range of elements in another range of elements. The former returns the first match, while the latter returns the last match.
+   - `binary_search()` checks whether a given element is present in a sorted range. By exploiting the fact that the elements in the input range are sorted, it can find the desired element faster than `find()`. Elements are compared using either the `<` operator or a user-provided comparison callback.

**Caution** Earlier in this chapter, we explained that set and map containers are really good at finding elements themselves already. Because they know the internal structure of their data, they can find elements much faster than any generic algorithm ever could. These containers therefore offer a `find()` member function that you should always use instead of the generic `std::find()` algorithm. In general, whenever a container offers member functions that are functionally equivalent to an algorithm, you should always use the former.

# Handling Multiple Output Values

`find()`, `find_if()`, `find_if_not()`—these three algorithms all search for the first element that meets a particular requirement. But what if you're interested in finding all of them instead? If you glance through all algorithms that the Standard Library has to offer, you'll find that there is no algorithm with a name like `find_all()`. Luckily, there are at least three algorithms that would allow you to obtain all elements in a given range that satisfy a given condition:

+   - `std::remove_if()` can be used to remove all elements that do not satisfy the condition. We discuss this algorithm in the next subsection.
+   - `std::partition()` rearranges the elements in a range such that those elements that satisfy a callback condition are moved to the front of the range and those that do not are moved to the back. We’ll leave this option for you to try later in the exercises.
+   - `std::copy_if()` can be used to copy all elements you need to a second output range.

```
```cpp
// Ex20_13.cpp — Extracting all odd numbers.
import <iostream>;
import <set>;
import <vector>;
import <algorithm>;

std::set<int> fillSet_intoN(size_t N);       // Fill a set with 1, 2, ..., N
void printVector(const std::vector<int>& v); // Print the contents of a vector to std::cout

int main()
{
    const size_t num_numbers{20};

    const auto numbers = fillSet_intoN(num_numbers);

    std::vector<int> odd_numbers( numbers.size() ); // Caution: not { numbers.size() } here!
}
```
```