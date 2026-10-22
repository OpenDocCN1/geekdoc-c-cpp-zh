```
std::cout << len("tmp"); // OK: len() for array is best match

std::vector<int> v;
std::cout << len(v); // OK: len() for a type with size_type is best match

int* p;
std::cout << len(p); // OK: only fallback len() matches

std::allocator<int> x;
std::cout << len(x); // ERROR: 2nd len() function matches best,
// but can’t call size() for x
```

See Section 15.7 on page 284 for more details about SFINAE and Section 19.4 on page 416 about some applications of SFINAE.

# SFINAE and Overload Resolution

Over time, the SFINAE principle has become so important and so prevalent among template designers that the abbreviation has become a verb. We say “we *SFINAE out a function*” if we mean to apply the SFINAE mechanism to ensure that function templates are ignored for certain constraints by instrumenting the template code to result in invalid code for these constraints. And whenever you read in the C++ standard that a function template “*shall not participate in overload resolution unless…*” it means that SFINAE is used to “SFINAE out” that function template for certain cases.

For example, class `std::thread` declares a constructor: [Click here to view code image](#)

```
namespace std {
class thread {
public:
...
template<typename F, typename... Args>
explicit thread(F&& f, Args&&... args);
...
};
}
```

with the following remark:

> *Remarks:* This constructor shall not participate in overload resolution if `decay_t<F>` is the same type as `std::thread`.

This means that the template constructor is ignored if it is called with a `std::thread` as first and only argument. The reason is that otherwise a