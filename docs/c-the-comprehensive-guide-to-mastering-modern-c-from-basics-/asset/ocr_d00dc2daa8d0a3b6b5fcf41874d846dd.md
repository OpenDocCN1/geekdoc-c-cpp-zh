implementation of index can take place. However, it is an implementation detail of the library, and thus impl_multimap.hpp is not found in the directory of qwort.hpp, as it is not shipped with it. It is located right to qwort.cpp and impl_multimap.hpp. You can see the source code itself in Listing 11.3.

```
// https://godbolt.com/z/ob9voovmX
#include <string>
#include <string_view>
#include <vector>
#include <map> // multimap
namespace qw::impl_multimap {

using std::vector; using std::multimap;
using std::string; using std::string_view;

class index_impl {
    vector<string> entries;
    multimap<string, size_t> qindex;

public:
    void add(string_view normalized, string_view original);
    string getBestMatch(string_view normalized) const;
    size_t size() const {
        return entries.size();
    }

private:
    vector<string> qramify(string_view normalized) const {
        static constexpr size_t O = 3;
        static const std::string PREFIX;
        static const std::string SUFFIX;
public:
    // test interface
    vector<string> qramify(string_view n) const { return qramify(n); }
    size_t size() { return 0; }
    static std::string prefix() { return PREFIX; }
    static std::string suffix() { return SUFFIX; }
};
} // namespace qw::impl_multimap
```

# Listing 11.3 Header of the implementation class.

Because the focus here is not really on the algorithm, I will keep it brief. In the entries vector, the index stores