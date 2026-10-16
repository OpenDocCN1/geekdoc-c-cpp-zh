```
f({10.0}); // function argument
return {11}; // returnvalue
}
```

The reason that an unqualified list is not allowed on the left-hand side of assignments is primarily that the C++ grammar allows `{` in that position for compound statements (blocks), so that readability would be a problem for humans and ambiguity resolution would be tricky for compilers. This is not an insurmountable problem, but it was decided not to extend C++ in that direction.

When used as the initializer for a named object without the use of a `=` (as for `v` above), an unqualified `{}`-list performs direct initialization (§16.2.6). In all other cases, it performs copy initialization (§16.2.6). In particular, the otherwise redundant `=` in an initializer restricts the set of initializations that can be performed with a given `{}`-list.

# Section 11.3.3 Unqualified Lists 289

The standard-library type `initializer_list<T>` is used to handle variable-length `{}`-lists (§12.2.2.3). Its most obvious use is to allow initializer lists for user-defined containers (§3.2.1.3), but it can also be used directly; for example:

```
int high_value(initializer_list<int> val)
{
int high = numeric_traits<int>::lowest(); if (val.size()==0) return high;
for (auto x : val)
if (x>high) high = x;
return high; }
int v1 = high_value({1,2,3,4,5,6,7});
int v2 = high_value({-1,2,v1,4,-9,20,v1});
```

A `{}`-list is the simplest way of dealing with homogeneous lists of varying lengths. However, beware that zero elements can be a special case. If so, that case should be handled by a default constructor (§17.3.3).

The type of a `{}`-list can be deduced (only) if all elements are of the same type. For example:

```
auto x0 = {}; // error (no element type)
auto x1 = {1}; // initializer_list<int>
auto x2 = {1,2}; // initializer_list<int>
auto x3 = {1,2,3}; // initializer_list<int>
auto x4 = {1,2,0}; // error : nonhomogeneous list
```

Unfortunately, we do not deduce the type of an unqualified list for a plain template argument. For example:

```
template<typename T>
void f(T);

f({}); // error : type of initializer is unknown
f({1}); // error : an unqualified list does not match “plain T”
f({1,2}); // error : an unqualified list does not match “plain T”
```