# Function Objects (a.k.a. Functors) 1027

In the general, the third argument could be a functor, not just a regular function. Actually, this raises a question: How do you declare the third argument? You can't declare it as a function pointer because function pointer specifies the argument. Because a container can contain just about any type, you don't know in what particular argument should be used. The STL solves that problem using templates. The for_each prototype looks like:

```
template<class InputIterator, class Function>
Function for_each(InputIterator first, InputIterator last, Function f);
```

The ShowReview() prototype is:
void ShowReview(const Review&);

This makes the identifier ShowReview have the type void (*const Review&), so that the type is assigned to the template argument. With a different function call, the argument could represent a class type that has an overloaded () operator. Ultimately, the for_each() code will have an expression f().
ShowReview() example is a pointer to a function, and f() invokes the function. If the final_each() argument is an object, then f() becomes the object that invokes it overloaded () operator.

# Functor Concepts

Just as the STL defines for containers and iterators, it defines functor concepts:

+   - A generator is a functor that can be called with no arguments.
- A unary function is a functor that can be called with one argument.
- A binary function is a functor that can be called with two arguments.

For example, the functor supplied to for_each() should be a unary function because it is applied to one element at a time.
Of course, these concepts come with refinements:

+   - A unary function that returns a bool value is a predicate.
- A binary function that returns a bool value is a binary predicate.

Several STL functions require predicate or binary predicates. For example,
Listing 16.9 uses a version of sort() that takes a binary predicate as its third argument:
bool WorseThan(const Review& r1, const Review& r2);
...
sort(books.begin(), books.end(), WorseThan);

The list template has a remove_if() method that takes a predicate as an argument.
It applies the predicate to each member in the indicated range, removing elements for which the predicate returns true. For example, the following code would remove all elements greater than 100 from the list three: