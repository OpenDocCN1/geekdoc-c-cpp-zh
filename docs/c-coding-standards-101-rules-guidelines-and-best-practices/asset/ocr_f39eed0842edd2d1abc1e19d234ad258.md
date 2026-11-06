# 88. Prefer function objects over functions as algorithm and comparer arguments.

# Summary

Objects plug in better than functions: Prefer passing function objects, not functions, to algorithms. Comparers for associative containers must be function objects. Function objects are adaptable and, counterintuitively, they typically produce faster code than functions.

# Discussion

First, function objects are easy to make adaptable, and always should be (see Item 89). Even if you already have a function, sometimes you have to wrap it in `ptr_fun` or `mem_fun` anyway to add adaptability. For example, you have to do this in order to build up more complex expressions using binders (see also Item 84):

```
inline bool IsHeavy( const Thing& ) { /*...*/ }
find_if( v.begin(), v.end(), not1( IsHeavy ) );          // error: isn’t adaptable
```

The usual workaround is to insert `ptr_fun` (or, for a member function, `mem_fun` or `mem_fun_ref`), which unfortunately doesn’t work in this particular case:

```
inline bool IsHeavy( const Thing& ) { /*...*/ }
find_if( v.begin(), v.end(), not1( ptr_fun( IsHeavy ) ) );  // a valiant attempt
```

It’s a pain that this wouldn’t work even if you explicitly specified `ptr_fun`’s template arguments. Briefly, the problem is that `ptr_fun` deduces the argument and return types exactly (in particular, the parameter type is deduced as `const Thing&`) and goes on to create internal machinery which, along the way, in turn helpfully tries to add another `&`, and references to references are not currently allowed by ISO C++. There are ways in which the standard language and/or library could, and probably should, be fixed so as to make this work correctly (e.g., by allowing references to references to collapse to a single reference; or see also Item 89), but it doesn’t do that today.

You don’t have to remember this stuff if you’re using a correctly-written function object (see Item 89), which is adaptable from the get-go without special syntax:

```
struct IsHeavy : unary_function<Thing, bool> {
    bool operator()( const Thing& ) const { /*...*/ }
};
find_if( v.begin(), v.end(), not1( IsHeavy() ) );          // ok: adaptable
```