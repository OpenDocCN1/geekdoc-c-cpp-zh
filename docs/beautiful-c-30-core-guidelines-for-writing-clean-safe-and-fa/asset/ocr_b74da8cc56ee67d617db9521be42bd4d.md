It’s time to introduce properly the Guidelines Support Library (GSL). This is a small library of facilities designed to support the Core Guidelines. There are a lot of items in the Core Guidelines, some of which are very hard to enforce. The use of raw pointers is a case in point: how do you signal ownership of a pointer if you can’t use smart pointers? The GSL provides types to aid enforcement.

The GSL is divided into five parts.

+   - GSL.view: these types allow the user to distinguish between owning and non-owning pointers, and between pointers to a single object and pointers to the first element of a sequence.
+   - GSL.owner: these are ownership pointers, which include std::unique_ptr and std::shared_ptr as well as stack_array (a stack allocated array) and dyn_array (a heap allocated array).
+   - GSL.assert: these foreshadow the contracts proposal by providing two macros, Expects and Ensures.
+   - GSL.util: no library is complete without a homeless bag of useful things.
+   - GSL.concept: this is a collection of type predicates.

The GSL predates C++17, and parts of the GSL, particularly the concept section, have been superseded by Standard C++. It’s available on GitHub at https://github.com/Microsoft/GSL. Simply #include <gsl/gsl> to get the full set of objects.

This chapter is most concerned with one of the view types, gsl::owner<T*>. Let’s look at an example:

Click here to view code image

```
#include <gsl/gsl>

gsl::owner<int*> produce()      // You will
become the proud owner
{
```