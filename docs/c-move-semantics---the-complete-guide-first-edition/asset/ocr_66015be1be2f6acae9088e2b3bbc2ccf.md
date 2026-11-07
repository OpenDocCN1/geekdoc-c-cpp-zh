# ### 14.3.2 Move Iterators in Constructors and Member Functions

You can also use move iterators wherever an algorithm that reads elements once is used. A useful scenario might be to move elements of a source container to another container (of the same or a different kind). For example:

*lib/moveitor.cpp*

```
```cpp
#include <iostream>
#include <string>
#include <list>
#include <vector>

template<typename T>
void print(const std::string& name, const T& coll)
{
    std::cout << name << " (" << coll.size() << " elems): ";
    for (const auto& elem : coll) {
        std::cout << " \"" << elem << "\"";
    }
    std::cout << "\n";
}

int main()
{
    std::list<std::string> src{"don't", "vote", "for", "liars"};

    // move all elements from the list to the vector:
    std::vector<std::string> vec{std::make_move_iterator(src.begin()),
                                 std::make_move_iterator(src.end())};

    print("src", src);
    print("vec", vec);
}
```
```

The program has the following output: (? signaling that we do not know the value):

```
```text
src (4 elems): "?" "?" "?" "?"
vec (4 elems): "don't" "vote" "for" "liars"
```
```

Note again that the number of elements in the source container did not change. We moved all elements to the initialized new container. Therefore, the elements in the source range are in a moved-from state afterwards and we do not know their values.