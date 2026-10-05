# 26.2.2 Output the Contents of a Container to a Stream

This recipe is needed repeatedly: for example, for debugging or during unit tests. Of course, there are a thousand ways to output the elements of a container to a stream: from a simple loop to a ranged for loop to a specialized overload of the operator<<.

The most elegant way, however, is to copy the contents of the container to the stream—for this, std::copy from <algorithm> is used, and std::copy before C++20. Then, all that is needed is ostream_iterator from <iterator> as an adapter, and the output is a one-liner:

```
// https://github.org/z/fGKsfs1Y4
#include <iostream> // cout
#include <algorithm> // copy
#include <iterator> // ostream_iterator
#include <vector>
int main() {
 std::vector<char> path;
 for (char ch = 'a'; ch <= 'z'; ++ch) {
  path.push_back(ch);
}
 std::ranges::copy(path, // here everything, but it also works with
 other ranges;
 std::ostream_iterator<char>(std::cout, " ") // copy to cout,
 separator = " ");
}
```

After reading the chapter on containers, you might think that array always has a fixed

# 26.2.3 So “array” Is Not That Static