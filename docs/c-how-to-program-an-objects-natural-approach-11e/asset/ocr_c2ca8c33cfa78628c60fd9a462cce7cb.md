+   - The metafunction class template in lines 20–23 matches only pointer types. For this purpose, we define a partial template specialization.<sup>103</sup> Unlike a full template specialization that begins with the template header `template<>`, a partial template specialization still specifies a template header (line 20) with one or more parameters, which it uses in the angle brackets following the class name (line 21). In this case, the partial specialization is that `T` must be a pointer—indicated with `T*`. To remove the `*` from the pointer type, the type alias in line 22 defines the type member simply as `T`.

Lines 36 and 38 in `main` demonstrate our custom `my_remove_ptr` type metafunctions. Let’s consider the compiler’s matching process for invoking them.

# Instantiating my_remove_pointer for Non-Pointer Types

The expression in line 36

```
`my_remove_ptr<int>::type`
```

instantiates the template with the non-pointer type `int`. The compiler must decide which definition of `my_remove_ptr` matches the expression. Since there is no `*` to indicate a pointer in the type `int`, this expression matches only the `my_remove_ptr` definition in lines 14–17, which sets its type member to the type argument `int`. To confirm this, we use `std::is_same_v` to compare type `int` to the type returned by the preceding expression. They are the same, so the result is true.

# Instantiating my_remove_pointer for Pointer Types

The expression in line 38

```
`my_remove_ptr<int*>::type`
```

instantiates the template with the pointer type `int*`, which can match both definitions of `my_remove_const`:

+   - the first definition can match any type
+   - the second can match any pointer type.

Again, the compiler always chooses the most specific matching template. In this case, the type `int*` matches the partial template specialization in lines 20–23:

+   - the `int` in the preceding expression matches `T` in line 21 and
+   - the `*` in the preceding expression matches the `*` in line 21, separating it from the type `int`—this is what enables the partial template specialization to remove the pointer (`*`) from the type.

To confirm that the `*` was removed, we use `std::is_same_v` to compare `int` to the type returned by the preceding expression. They are the same, so the result is true.

# Adding lvalue and rvalue References to a Type

The predefined type metafunctions that modify types work similarly to `my_add_const` and `my_remove_ptr` type metafunctions. Lines 43 and 45 in `main` demonstrate the predefined type metafunctions `add_lvalue_reference` and `add_rvalue_reference`. Line

103. Iñbal Levi, “Exploration of C++20 Metaprogramming,” September 29, 2020. Accessed April 18, 2022. https://www.youtube.com/watch?v=XgrjybKaIV8.