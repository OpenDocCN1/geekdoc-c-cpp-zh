
## Working further from the metal

Things are different for me now. C++ takes me very close to the metal, but not on the metal. The compiler bridges that gap and embodies all the detailed knowledge that I used to have about the Z80 processor. In my current case that knowledge concerns the x86-64 architecture, which encompasses multiple processors. I cannot hope to acquire the necessary detail on my own. This is one of the reasons for moving to C++.

There is an art to optimization, but there is also an art to developing code that can be optimized well. You cannot optimize code that is utterly inflexible, and optimized code will often end up in this state. Optimizable code leaves options for the optimizer, be that a human or a compiler. Code that can be optimized is code with options to change things. Indeed, the words “optimize” and “option” both have the same Latin root, optare, “to choose.”

Engineers tend to optimize code in two ways, either by improving the design or by improving the performance. Improving the design means improving the comprehensibility and reusability of the code or responding to refinements to the requirements. Improving the performance means giving the compiler the greatest amount of information about what it is that you want to do and the greatest range of options to improve the performance.

The Core Guidelines page offers a good example from the C standard, which we reproduce here:

```c++
void qsort(void* base, size_t num, size_t size,
    int(*comp)(const void*, const void*));
```

This function takes a pointer to some memory, the number of things you want to sort, the size of the things you want to sort, and a function for ordering the things you want to sort.

Let’s start with optimizing the design of this function. The first problem is that we seem to be sorting memory rather than sorting things. This is the wrong level of abstraction. If you’re going to name a function “sort,” then the implication is that you will be sorting things. The idea of sorting memory is meaningless. Also, by taking a void*, the function is discarding information known at the call site: the type of object.

We can fix this immediately by jumping to C++ and exchanging the void* for a template parameter:

```c++
template <typename T>
void sort(T* base, size_t num, size_t size,
    int(*comp)(const T*, const T*));
```

This optimization improves the design by catching a typical error at compile time rather than runtime: passing a nonsensical comparison function. A void* can point to anything at all, while a T* must point to an instance of T. If you had a set of floating-point values that you wanted to sort, and your comparison function sorted characters, a call to sort may yield the wrong result.

Next, consider the two size_t parameters. First, they are an accident waiting to happen. The client must take care to pass these parameters in the correct order; they will get no warning from the compiler if they get this wrong. However, the size parameter is now redundant. Since the type being sorted is now part of the function signature, the size is known at compile time. The signature now looks like this:

```c++
template <typename T>
void sort(T* base, size_t num, int(*comp)(const T*, const T*));
```

Specializing the function over the type gives the compiler more information. There may be optimizations available if the total volume of memory occupied by the objects being sorted is less than, for example, the size of the L1 cache.

The final parameter is a function pointer. This is a callback function. The sort function will invoke this when it needs to decide the order of two objects. Optimizations are hard to come by here, but since sort is now a function template, it is reasonable to hope that the function will be instantiated at compile time. If the callback function definition is visible to the sort function, it may be inlined into the function template specialization.

There is a better solution, which is to make the callback function a template parameter. Consider this signature:

```c++
template <typename T, typename F>
void sort(T* base, size_t num, F fn);
```

There are going to be some restrictions on F. It needs to be invocable, taking two T* s and returning a negative integer value if the first argument precedes the second, zero if they are equal, and a positive integer value otherwise. After all, this is what the original function pointer did. However, we can now pass a lambda function rather than a function pointer, which makes inlining much more likely. We can also pass a std::function object, or even a member function pointer.

Of course, since we know that values will be passed to this function, we can usefully constrain the function still further and take a pair of T const&s, allowing a broader range of functions to be passed and eliminating the need to test for null pointers. This is yet more information for the compiler to work with, and yet more opportunity for optimization.

What next? Well, the first two parameters are now a little suspicious. The qsort function requires that the items being sorted lie in contiguous memory. This gives us a few advantages. First, we can simply pass a pair of iterators. In all probability, you are starting off with a pair of iterators anyway, and using std::distance to calculate the number of elements. Working at the correct level of abstraction, you should pass in the range of values you want to sort:

```c++
template <typename InIt, typename F>
void sort(InIt first, InIt last, F fn);
```

This is a safer spelling because you do not have to concern yourself with any arithmetic. You only need to tell the function what the ends of the range are. This provides a design optimization by reducing the opportunity for error, as well as a compilation optimization by announcing the addresses of the first and last elements, rather than requiring the compiler to emit code to calculate them. We can further improve the design by adding requires clauses now that we are in the brave new world of C++20. In fact, we can do even better than that and exchange the iterator pair for a range:

```c++
template <typename R, typename F>
void sort(R&& r, F fn);
```

Now we can add meaningful constraints, simplifying the design still further and giving the compiler yet more information, by using the random_access_range concept:

```c++
template <std::ranges::random_access_range R,
         typename F>
void sort(R&& r, F fn);
```

As we are sure you have guessed by now, what we have done here is followed the evolution of sort from its pre-C++ incarnation to its C++20 incarnation. You can still find qsort in the standard library, but there is very little reason to use it outside of legacy environments. The function signature quoted above is not from the standard; ranges work with projections, which are beyond the scope of this chapter. For completeness, this is what one of the overloads looks like:

```c++
template <std::ranges::random_access_range R,
         typename Comp = std::ranges::less,
         typename Proj = std::identity>
requires std::sortable<std::ranges::iterator_t<R>, Comp, Proj>
constexpr std::ranges::borrowed_iterator_t<R>
sort(R&& r, Comp comp={}, Proj proj={});
```

This function:

- Takes a range, a comparison function, and a projection
- Requires that the range can be sorted with instances of the supplied types
- Is a constexpr function
- Returns an iterator to the final element

This function also gives the compiler much more information than qsort and enables a clearer call site.

However, you may look at that fistful of characters and contemplate the considerable increase in the size of the declaration. You will, unfortunately, also experience an increase in compilation time. Rather than, as with qsort, simply inserting a function call at the call site, the compiler will first infer the template parameters, ratify the constraints, instantiate then optimize the function template, and consider the value of inlining. You are exchanging run-time execution for compile-time execution.

Making things faster takes time. Spend that time: it is a wise investment. Be prepared to change your designs to facilitate performance improvements. However, don’t dive in with the virtual stopwatch combing through every function. Let’s first establish if you need to make that investment.

## Optimization through abstraction

Recall the title of this chapter: “Design to enable optimization.” The set of steps just taken could just as well have been included in a chapter on abstraction. Not only did we potentially improve the performance characteristics of the function, but we also improved the abstraction of the
