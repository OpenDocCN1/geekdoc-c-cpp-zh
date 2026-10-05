because id_is_const—just if you had passed it as a parameter to the function.

Use const variables when it seems sensible to you, with discretion. For variables that are valid in a long section of code, where it is easy to lose track of which variables exist at all, const can be an effective protection against accidental modification.

```
// https://godbolt.org/bxPaz9aW5
#include <vector>
namespace {
    const unsigned DATA_SIZE = 100; // number of elements in data */
    const double LIMIT = 999.999; // * max value during initialization */
}
std::vector<int> createData(DATA_SIZE) {
    double currVal = 1.0;
    for(auto &elem : result) {
        elem = currVal; // next value is large
        if(currVal > LIMIT) {
            currVal = LIMIT; // no value should be large
        }
    }
    return result;
}
```

# **Listing 13.8** Local constants of a file fit well into an anonymous namespace.

This is especially true for global variables, for example, define certain program parameters. It is best to put them in an anonymous namespace. The effect of this is that the identifier cannot be seen by other modules; in large projects, this is important to prevent global variables and constants from conflicting.

This allows you to easily tweak certain sizes of the program while also documenting the size well.