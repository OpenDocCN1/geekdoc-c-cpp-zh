
That error code may be ignored entirely. The problem of ignoring return codes in the general case has been partially solved with the addition of the [[no_discard]] attribute, but this is only useful if you are exclusively using the return value for returning errors. Even then, the caller may store the return value and forget to consider it. Forcing users to check for errors is a bad idea anyway: it is for them to decide how to deal with failure, not you.

The trouble is that there are more ways for code to go wrong than to perform correctly. Much like the human body, we can identify when it is in good working order, but identifying the myriad ways in which it can fail is a tall order.

## Light at the end of the tunnel

We mentioned that the Boost solutions have not been standardized and are only available where use of Boost is permitted. The committee is considering several papers to improve matters. The first of these proposes std::expected<T, E>, which is a type that may contain a value of type T, or a value of type E, which represents the reason why a value of type T is not present. It is rather like a specialized version of std::variant. This was first proposed shortly after C++14 was finalized, so it has spent a long time being considered. You can check progress by examining paper P0323.4

4. www.open-std.org/jtc1/sc22/wg21/docs/papers/2021/p0323r10.html

Next, we have zero-overhead deterministic exceptions, which throw values rather than types. This paper addresses the divided C++ community by making exception handling much more palatable. Particularly, the values that are thrown are stack allocated and statically typed, which means no heap allocation is required and RTTI is not used. They are like a special return type. You can check progress by examining paper P0709.5 Note that Boost.Outcome is a partial, library-only implementation of this idea. Language changes will need to be made to fully implement it.

5. www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p0709r4.pdf

The third paper under consideration proposes a new status_code and standard error object. This operates with zero-overhead deterministic exceptions. It offers some improvements over the <system_error> header, such as not including the <string> header, which brings with it a large quantity of additional machinery such as allocators and algorithms, greatly increasing build and link times.

One aspect of error handling we have yet to mention is the use of the assert macro. This is a way of discovering instances of the second type of error described in the previous section. It highlights what the programmer is expecting to be the state of the abstract machine at a particular instant and directs the program to stop execution if that state turns out to be different. This is different from a broken abstract machine: this is the programmer getting things wrong.

As a development of this idea, there is yet another proposal under consideration which very nearly made it into C++20. In fact, it got as far as the working draft before being pulled out at the last minute. We are talking about contracts. These define pre- and post-conditions in the language rather than as a library macro, by decorating the function definition with programmer-defined expectations.

Unfortunately, this cornucopia of upgrades to the language and library is yet to be emptied into the C++ Standard working draft at time of writing. Today, in the community of C++ users, things have remained largely unchanged for many years. Programmers are still using old C-style error-handling strategies for want of a better option. The future looks bright, but it has yet to arrive.

## Summary

In summary:

- Global state is a bad place to handle errors. Keep error state local and pay attention to it.
- If you can throw and catch exceptions, do so.
- Differentiate between different types of error: bad input, bad logic, bad environment, and so on.
- If exception handling is not available to you, consider using Boost.Outcome, but pay attention to upcoming changes to the standard; the Core Guidelines do not cover this approach since it is outside the scope of the standard.

## Chapter 3.6

## SF.7: Don’t write using namespace at global scope in a header file

## Don’t do this

Please, don’t do this. Ever.

Never. Not ever. Not even once.

Please.

The Core Guidelines document offers the following example:

Click here to view code image

```cpp
// bad.h
#include <iostream>
using namespace std; // bad <- "You're not kidding," says Guy

// user.cpp
#include "bad.h"

// some function that happens to be named copy
bool copy(/*... some parameters ...*/);

int main()
{
    // now overloads local ::copy and std::copy,
    could be ambiguous
```

```
copy(/*...*/);
}
```

“Bad” is an understatement. We know it seems we are belaboring the point, but this example only exposes part of the horror.

## Disambiguation

There is one and only one global namespace. From the standard, [basic.scope.namespace]¹:

1. https://eel.is/c++draft/basic.scope.namespace

> “The outermost declarative region of a translation unit is also a namespace, called the global namespace. A name declared in the global namespace has global namespace scope (also called global scope). The potential scope of such a name begins at its point of declaration and ends at the end of the translation unit that is its declarative region. A name with global namespace scope is said to be a global name.”

> Do not pollute the global namespace: it is a precious resource.

Do not pollute the global namespace: it is a precious resource.
Namespaces are a useful encapsulation tool, collecting together related symbols within a single scope and enabling the reuse of names. My favorite example is vector. This has two meanings in my domain: there is the automatically resizing contiguous container, and there is the tuple of numbers representing a mathematical quantity. The former lives in namespace std, while the latter lives somewhere else. In my case, it lives in namespace gdg::maths. Namespace gdg is my personal namespace that I use in all my code, while namespace maths is contained within that and consists of mathematical types and functions, like matrix, vector, normalize, intersect, and all the other types you might need for

geometry. I am British, so I say “maths.” Ask me about it one day if you dare.

Having two classes called vector is not a problem, since we can simply apply namespace scope resolution to the symbol, and type std::vector when we want to contain things in the maths namespace and type gdg::maths::vector when we want to manipulate geometric objects outside of the maths namespace.

std:: is not much to type for disambiguation purposes. On the other hand, gdg::maths:: is a little long. It interferes with rapid apprehension of code. The excessive colons slightly disrupt reading. Fortunately, we can type

```
using gdg::maths::vector;
```

earlier in the scope and the compiler will choose that vector over std::vector when it tries to resolve the symbol. This is known as a using-declaration. It is distinct from typing

```
using namespace gdg::maths;
```

which is a using-directive.

The trouble with introducing a using-directive into a header file at global scope is clear for all to see: you have hidden from the user the fact that all the symbols in the namespace have been introduced into the parent scope of every function and class definition. Worse, if you introduce a different using-directive into a different header file and include both of those header files, they become order dependent. You will get subtly different compilation if you change their order.

Unfortunately, this is only the start of the madness.

## Using using

The keyword using has four uses. The first is aliasing. For example:

Click here to view code image

```
using vector_of_vectors =
std::vector<gdg::maths::vector>;
```

This is very specific. We are introducing a new name as an abbreviation for another name. Here, we are introducing the name vector_of_vectors to directly map to a standard vector of my maths vectors. We are using using in this way to reduce typing and improve clarity.

The second is for importing class members. For example:

Click here to view code image

```
struct maths_vector : std::variant<vector<float,
2>, vector<int, 2>> {
    using variant::variant;
}
```

Here, we are introducing a member of a base class into a derived class. This allows me to construct a maths_vector object using a variant constructor.

The third is for introducing names defined elsewhere into the declarative region of the using-declaration. For example:

Click here to view code image

```
namespace gdg::maths {
    using std::inner_product;
}
```

We can now call the standard version of inner_product from within the gdg::maths namespace without having to prefix it with std. If the name already existed in an outer scope, it is hidden by this new declaration. If we wanted to call a different inner_product function we would have to qualify it.

Using-declarations are more specific than using-directives. They introduce a single symbol into the current scope. Still, using-declarations should be used with care, at the narrowest comfortable scope. Making a using-declaration may also create an overload set, so make sure it is always
