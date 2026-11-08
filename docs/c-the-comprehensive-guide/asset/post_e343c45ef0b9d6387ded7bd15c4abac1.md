
```cpp
namespace qw::impl_multimap {

using std::vector; using std::multimap; using std::map; using std::string;
using std::string_view; using namespace std::literals::string_literals;

void index_impl::add(string_view normalized, string_view original) {
    /* TODO: Check for existence in 'entries' */
    const auto pos = entries.size(); // Index of the new entry
    entries.push_back(string(original));
    auto qgrams = qgramify(normalized);
    for(const auto& qgram : qgrams) {
        qindex.insert( make_pair(qgram, pos) );
    }
}

string index_impl::getBestMatch(string_view normalized) const {
    auto qgrams = qgramify(normalized);

    /* hits stores which words were hit how often */
    map<size_t, size_t> hits; /* 'entries-index' to 'hit-count' */
    size_t maxhits = 0; /* always: max(hits.second) */
    for(const auto& qgram : qgrams) {
        auto [beg, end] = qindex.equal_range(qgram);
        for(auto it=beg; it!=end; ++it) {
            hits[it->second] += 1; /* hit-count of the entry */
            if(hits[it->second] > maxhits) { /* simpler max-search */
                maxhits = hits[it->second];
            }
        }
    }

    /* Search first entry with maxhits. Improvement possible with PrioQueue */
    for(auto const & hit : hits) {
        if(hit.second == maxhits) {
            return entries[hit.first];
        }
    }

    /* only reached if entries is empty */
    return ""s;
}
const string index_impl::PREFIX = string(Q-1, '^');
const string index_impl::SUFFIX = string(Q-1, '$');

vector<string> index_impl::qgramify(string_view normalized) const {
    auto word = PREFIX+string(normalized)+SUFFIX; /* trick for better q-grams */
    vector<string> result {};
    auto left = word.cbegin();
    auto right = std::next(word.cbegin(), Q); /* okay: ["^"|"$"] = 3 */
    for(; right <= word.end(); ++left, ++right) {
        result.emplace_back(left, right);
    }
    return result;
}
} // namespace qw::impl_multimap
```

**Listing 11.4** The heart of the implementation class.

As I said before, for this chapter, exactly how the algorithm is implemented is not so interesting. For the module, it is much more important that everything works as it should externally. Nevertheless, I would like to say a few words about the structure of this implementation file.

As always, I include the header of what is implemented in this file as early as possible. Then, only the necessary headers of the standard library follow.

The defined methods all belong to the `qw::impl_multimap` namespace, which is opened at the beginning and closed at the end.

`add()` stores the entry in `entries` and `qindex` after it has been dissected using `qgramify()`. In one aspect, this implementation of `add()` behaves poorly: if you store exactly the same entry twice, you will never find one of them again. So it would be good if `add()` checked whether the entry already exists before storing it, or if a search would find not only the best match but somehow also several good matches. However, I leave solving this problem to your tinkering spirit.

`getBestMatch()` also breaks down the search pattern using `qgramify()` into its components. In this, it counts how often each original word was matched. At the end, the entry with the highest number of matches is selected and returned.

In `qgramify()`, I use a simple trick to slightly increase the number of generated q-grams: the entry or search pattern is framed by `^^` and `$$` before being broken down. As a result, the list of q-grams for words of length three like NYC includes not only NYC, but also `^^N`, `NYC`, and `C$$`, thus having better chances of being matched.

All in all, creating q-grams for a similarity index is neither a very difficult task nor a perfect solution. There are many algorithms that achieve better results with more sophisticated methods. But for its simplicity, the q-gram index delivers surprisingly good results.

This entire functionality is then packaged into the `qwort.a` library. On other systems, it may also be called `qwort.so`, `qwort.lib`, or `qwort.dll`. Together with the `qwort/qwort.hpp` header and documentation, this is the minimum delivery package for the customer.

### 11.4.3 Using the Library

Because you are my customers today, I will demonstrate how you can use the library in a program before we move on to the tests. Listing 11.5 is pretty much the simplest example program to demonstrate the library.

After the `include` and `using` directives, the `main` program follows immediately. First, two example entries are stored in the index. Then follows a loop over all command line arguments of the program. For each argument, a search for the best match is performed, which is then output.

```cpp
// https://godbolt.org/z/jz9TshnY (includes all files)
#include <cstdlib>  // EXIT_SUCCESS
#include <iostream> // cout
#include <vector>
#include <string>
#include "qwort/qwort.hpp"

using std::cout; using std::vector; using std::string;

int main(int argc, const char* argv[]) {
    cout << "qwort version " << qw::version() << "\n";

    /* Build index */
    qw::index myindex{};

    /* Demo data */
    myindex.add("Germany");
    myindex.add("Greece");

    /* Generate queries */
    vector<string> args(argv+1, argv+argc); // iterator-based initialization
    for(auto &querystring : args) {
        cout << "Searching for '" << querystring << "'... ";
        const auto match = myindex.getBestMatch(querystring);
        cout << match << "\n";
    }
    return EXIT_SUCCESS;
}
```

**Listing 11.5** Pretty much the simplest example program of the library.

The compiler packs this `query.cpp` source file with `qwort.hpp` (because it is included) and the `qwort.a` library together into the `query.x` program. The Makefile essentially says the following (somewhat obfuscated by variables):

```sh
g++ -o query.x query.cpp -lqwort -I../../include -L../lib
```

This means something like, “Create `query.x` from `query.cpp`, use the `qwort` library, and look for includes and libraries in the specified paths.”

If you run this program as follows, you will get this output:

```
$ ./query.x armada green
qwort version 1
Searching for 'armada'... Germany
Searching for 'green'... Greece
```

In the downloadable content at *www.rheinwerk-computing.com/5927*, you will find another simple example in `code/15p-lunittest-200/src/prog/dictfile.cpp`. There I create the index from lines of any text file. With additional command line parameters, you can then output the best matching lines.

## PART II
### Object-Oriented Programming and More

It's time for you to start building your own data types. This is the real strength of C++. You can simply bundle multiple pieces of data together so that you can treat them as one. More importantly, you can design classes where data and behavior form a single unit. This ultimately leads you to learn about object-oriented inheritance.

In this part, you’ll also learn more about constant and static values, as these become particularly interesting in the context of classes.

## Chapter 12: From Structure to Class

### Chapter Telegram

- **Aggregate**: An aggregate is a simple bundling of multiple data fields into a new type—specifically, a `struct` that only has data fields and methods. A C-array is also an aggregate.
- **struct**: A struct is a bundling of data fields. It may also have constructors, and private and static elements. It can be a simple aggregate or a more advanced structure.
- **class**: A class is very similar to a struct, except that class starts with private visibility; in common usage, a struct is more data-focused, while a class is more behavior-oriented.
- **Structure**: A structure can be more than an aggregate; for example, it can have constructors. When I speak of a *structure*, I usually refer to both `struct` and `class`.
- **Data field, member variable, or attribute**: A variable within a structure.
- **Method, member function, or instance function**: A function that is bound to its structure.
- **Member**: Generic term for data fields and methods of a class.
- **Constructor**: A special method for initializing a structure.
- **Inline**: Give the compiler a hint to insert the code directly instead of using a function call.
- **Include guard**: Avoid double inclusion.
- **public and private**: Protect methods and data fields from external access.
- **Encapsulation**: The clean separation of interface and implementation; possible in varying degrees.
- **Class as value**: Use the instance of a class as a value parameter (call-by-value) or as a return value.
