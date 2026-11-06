
- Start with the keyword `template`.
- Next, an empty set of angle brackets is written. This indicates to the compiler that there must be an *existing* template whose prototype matches the one we're about to define. If we err and there is no such template then the compiler reports an error like:

    ```
    error: template-id 'add<char*>' for 'char* add(char* const&, char*
            const&)' does not match any template declaration
    ```

- Now the function's head is defined. It must match the prototype of the initial function template or the form of a template explicit instantiation declaration (see section 20.5.1) if its specialized type cannot be determined from the function's arguments. It must specify the correct return type, function name, maybe explicit template type arguments, as well as the function's parameter list.
- Finally the function's body is defined, providing the special implementation that is required for the specialization.

Here are two explicit specializations for the function template `add`, expecting `char *` and `char const *` arguments:

```
template <> char *add<char *>(char *const &p1,
                              char *const &p2)
{
    std::string str(p1);
    str += p2;
    return strcpy(new char[str.length() + 1], str.c_str());
}

template <> char const *add<char const *>(char const *const &p1,
                                          char const *const &p2)
{
    static std::string str;
    str = p1;
    str += p2;
    return str.c_str();
}
```

Template explicit specializations are normally included in the file containing the other function template's implementations.

### 20.9.2 Declaring specializations

Template explicit specializations can be declared in the usual way. I.e., by replacing its body with a semicolon.

When *declaring* a template explicit specialization the pair of angle brackets following the `template` keyword are essential. If omitted, we would have constructed a template instantiation declaration. The compiler would silently process it, at the expense of a somewhat longer compilation time.

When declaring a template explicit specialization (or when using an instantiation declaration) the explicit specification of the template type parameters can be omitted if the compiler is able to deduce these types from the function's arguments. As this is the case with the `char (const) *` specializations, they could also be declared as follows:

```
template <> char *add(char *const &p1, char *const &p2);
template <> char const *add(char const *const &p1,
                            char const *const &p2);
```

If in addition `template <>` could be omitted the template character would be removed from the declaration. The resulting declaration is now a mere function declaration. This is not an error: function templates and ordinary (non-template) functions may mutually overload each other. Ordinary functions are not as restrictive as function templates with respect to allowed type conversions. This could be a reason to overload a template with an ordinary function every once in a while.

A function template explicit specialization is not just another overloaded version of the function template. Whereas an overloaded version may define a completely different set of template parameters, a specialization must use the same set of template parameters as its non-specialized variant. The compiler uses the specialization in situations where the actual template arguments match the types defined by the specialization (following the rule that the most specialized set of parameters matching a set of arguments will be used). For different sets of parameters overloaded versions of functions (or function templates) must be used.

### 20.9.3 Complications when using the insertion operator

Now that we’ve covered explicit specializations and overloading let’s consider what happens when a class defines a `std::string` conversion operator (cf. section 11.3).

A conversion operator is guaranteed to be used as an rvalue. This means that objects of a class defining a string conversion operator can be assigned to, e.g., string objects. But when trying to insert objects defining string conversion operators into streams then the compiler complains that we’re attempting to insert an inappropriate type into an ostream.

On the other hand, when this class defines an `int` conversion operator insertion is performed flawlessly.

The reason for this distinction is that `operator<<` is defined as a plain (free) function when inserting a basic type (like `int`) but it is defined as a function template when inserting a `string`. Hence, when trying to insert an object of our class defining a string conversion operator the compiler visits all overloaded versions of insertion operators inserting into `ostream` objects.

Since no basic type conversion is available the basic type insertion operators can’t be used. Since the available conversions for template arguments do not allow the compiler to look for conversion operators our class defining the string conversion operator cannot be inserted into an `ostream`.

If it should be possible to insert objects of such a class into ostream objects the class must define its own overloaded insertion operator (in addition to the string conversion operator that was required to use the class’s objects as rvalue in string assignments).

## 20.10 Static assertions (C++11)

The `static_assert(constant expression, error message)` utility is defined by the C++11 standard to allow assertions to be made within template definitions. Here are two examples of its use:

```
static_assert(BUFSIZE1 == BUFSIZE2,
             "BUFSIZE1 and BUFSIZE2 must be equal");

template <typename Type1, typename Type2>
void rawswap(Type1 &type1, Type2 &type2)
{
    static_assert(sizeof(Type1) == sizeof(Type2),
                  "rawswap: Type1 and Type2 must have equal sizes");
    // ...
}
```

The first example shows how to avoid yet another preprocessor directive (in this case the #error directive).

The second example shows how static_assert can be used to ensure that a template operates under the right condition(s).

The string defined in static_assert’s second argument is displayed and compilation stops if the condition specified in static_assert’s first argument is false.

Like the #error preprocessor directive static_assert is a compile-time matter that doesn’t have any effect on the run-time efficiency of the code in which it is used.

## 20.11 Numeric limits

The header file `<limits>` defines constants for various types, e.g., INT_MAX defines the maximum value that can be stored in an int.

The disadvantage of the limits defined in `climits` is that they are fixed limits. Let’s assume you write a function template that receives an argument of a certain type. E.g.,

```
template<typename Type>
Type operation(Type &&type);
```

Assume this function should return the largest negative value for Type if type is a negative value and the largest positive value if type is a positive value. However, 0 should be returned if the type is not an integral value.

How to proceed?

Since the constants in climits can only be used if the type to use is already known, the only approach seems to be to create function template specializations for the various integral types, like:

```
template<>
int operation<int>(int &&type)
{
    return type < 0 ? INT_MIN : INT_MAX;
}
```

The facilities provided by numeric_limits provide an alternative. To use these facilities the `<limits>` header file must be included.

The class template numeric_limits offers various members answering all kinds of questions that could be asked of numeric types. Before introducing these members, let’s have a look at how we could implement the operation function template as just one single function template:

```
template<typename Type>
Type operation(Type &&type)
{
    return
        not numeric_limits<Type>::is_integer ? 0 :
        type < 0 ? numeric_limits<Type>::min() :
                   numeric_limits<Type>::max();
}
```
