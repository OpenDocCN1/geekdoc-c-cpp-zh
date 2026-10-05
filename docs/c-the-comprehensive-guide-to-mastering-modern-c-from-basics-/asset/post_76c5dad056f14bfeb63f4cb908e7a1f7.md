
```cpp
for(auto c : word) std::cout << c;
std::cout << "]";
// Output: [The] [text] [is] [short]
```

# Listing 25.9 Searching with a predicate.

Here I use find_if first to skip spaces before a word in a string. find_if takes—like all algorithms—a range in which it should search. The range is defined by two iterators, the beginning and the end. The end always points to an element behind the last element of the range, so the empty range can always be specified by two identical iterators. Also useful: the number of elements in the range is simply the distance between the two iterators.

The last parameter in find_if is the if, which is the predicate. Here, I define a lambda that checks if the character of the string is not a whitespace, meaning the start of the next word is found. The second call to find_if uses a comparison with a whitespace as the predicate, which is after the end of the word. I then copy the range enclosed by these two positions as a new string into the result result using push_back.

However, with the introduction of ranges in C++20, a new split function was added, which makes the process somewhat simpler. Instead of returning a vector of string, the return type of split is word, which is a ranges::subrange within text. I then output character by character using c.

In another example, I would like to demonstrate the good interaction of iterators with algorithms. Cleverly combined, you get powerful tools. The function itPalindrome checks if a string reads the same forward and backward. You can implement this as a one-liner.

```cpp
// https://github.com/org/z/MKxnGdrbr
#include <algorithm>
#include <iostream>
#include <vector>
#include <string>
#include <string_view>

using std::string_view; using namespace std::literals; using std::cout;
auto isPalindrome(string_view sv) {
    return equal(sv.begin(), sv.end(), sv.rbegin());
}
int main() {
    for(auto s : {"madam"sv, "aibohphobia"sv, "abakadabra"sv}) {
        cout << s << " is " << (isPalindrome(s)?" not":"not a") << "\n";
    }
    return 0;
}
```

# Listing 25.10 Recognizing a palindrome with a single line of code.

The equal algorithm takes a range, through which it iterates, as its first two parameters. The third parameter is the beginning of a second range, with which the first range is then compared element-wise using ==. If all elements are equal, equal returns true; at the first difference, it returns false. The clever part here is that the beginning of the second range is passed with s.rbegin(). rbegin() returns an iterator that, when incremented with ++, moves one element backward. So the same sequence is traversed backward here. In the end, the first letter is compared with the last, then with the second-to-last, and so on.

We don't necessarily have to restrict isPalindrome to string_view. We could allow allow input_range auto&& as a parameter, and the function would work with any range and container that supports rbegin(). If I were more careful, I wouldn't traverse the entire sequence from start to finish, but only up to the halfway point, because == should be symmetric. I could achieve this by writing the following instead of s.end(): s.begin()+(s.end()-s.begin())/2.

In the case of for_each, information is not the goal; rather, a unary function without a return value is called on each element. Actually, these functions are intended to be read-only. However, if you provide an (in)appropriate functor or predicate, you can indeed modify the elements of the range. So doing so is forbidden but probably confusing. With for_each, you can see an example in Listing 25.11. Instead, you should use transform here.

```cpp
// https://godbot.org/z/iz1Ggo7d9
#include <iostream>
#include <vector>
#include <algorithm>
int main() {
    std::vector<int> c{1,2,3,4};
    std::for_each(c, [](auto &n) { n*=n; }); // Not modifying
    std::cout << c[3] << "\n"; // Output: 16
}
```

**Listing 25.11** Even "read-only" algorithms like "for_each" can modify elements.

That is why I want to emphasize one thing: do not use for_each to solve every problem. There are often algorithms that are better at solving certain problems. And if you look at the list of algorithms from time to time, you will become more comfortable with them over time, your code will become more compact and—I claim—better. A few examples:

- If you want to determine how often an element is contained in a sequence, use count, not for_each.
- If you want to check a predicate for all elements, use all_of.
- If you want to know if at least one element satisfies a predicate, use any_of.
- If a sequence contains the same elements as another, just in a different order, by no means use for_each; instead, use is_permutation.

These are the available non-modifying algorithms:

- all_of
Usage: frequent; iterators: Checks if a predicate is true for all elements.
- any_of
Usage: frequent; iterators: Checks if at least one element satisfies the predicate.
- none_of
Usage: frequent; iterators: Checks if none of the elements satisfy the predicate.
- for_each
Usage: frequent; iterators: Applies a unary function to each element.
- for_each_n
Usage: rare; iterators: Applies a unary function to the first n elements.
- find
Usage: constant; iterators: Finds the position of a sample value.
- find_if
Usage: frequent; iterators: Finds the position where a predicate matches.
- find_if_not
Usage: frequent; iterators: Finds the position by the negation of a predicate.
- find_end
Usage: rare; iterators: Finds the end of a subsequence.
- find_first_of
Usage: frequent; iterators: Finds one of several values.
- find_last
Usage: rare; iterators: Finds the last element matching the predicate.
- find_last_if
Usage: rare; iterators: Finds the last element matching the predicate. 
- adjacent_find
Usage: occasional; iterators: Finds the first position where adjacent elements both satisfy a predicate.
- count
Usage: constant; iterators: Counts the number of occurrences of a sample value.
- count_if
Usage: constant; iterators: Counts how often a predicate matches.
- mismatch
Usage: frequent; iterators: Finds the first difference between two sequences.
- equal
Usage: constant; iterators: Checks if all elements are pairwise equal.
- is_permutation
Usage: occasional; iterators: Is one sequence just a permutation of another?
- search
Usage: frequent; iterators: Finds the position where a subsequence is hidden within a larger sequence.
- search_n
Usage: occasional; iterators: Finds the position with n consecutive values equal to the sought value.
- contains, contains_subrange
Usage: frequent (C++23); iterators: Checks whether a single element or an entire range is contained within another.
- starts_with
Usage: frequent (C++23); iterators: Checks if one range starts with another.
- ends_with
Usage: frequent (C++23); iterators: Checks if one range ends with another.

## 25.6.4 Inherently Modifying Algorithms

functions in this section write a result to an output range. For some of the algorithms, it is allowed for the output range and input range to overlap. This is not always the case, so be careful and check the documentation to see if overlapping is allowed. Some algorithms like unique modify the sequence in place.
