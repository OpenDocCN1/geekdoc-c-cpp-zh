either in computation time or resource usage. However, some specializations of algorithms also provide more functionality, such as (in this case) the ability to move backward in a sequence.

While a conversion function template does have a return type—the type it is converting to—the template parameters in that type need to be deducible (see Chapter 15) for the conversion function template to behave properly.

In C++17, one can eliminate the recursion with pack expansions in the base class list and in a using declaration (Section 4.4.5 on page 65). We demonstrate this technique in Section 26.4 on page 611.

It would be slightly better to provide no result in the case of failure, to make this a SFINAE-friendly trait (see Section 19.4.4 on page 424). Moreover, a robust implementation would wrap the return type in something like `Identity`, because there are some types—such as array and function types—that can be parameter types but not return types. We omit these improvements for the sake of brevity and readability.

C++11 introduced the notion of contextual conversion to `bool` along with explicit conversion operators. Together, they replace uses of the “safe bool” idiom ([KarlssonSafeBool]), which typically involves an (implicit) user-defined conversion to a pointer-to-data member. The pointer-to-data member is used because it can be treated as a `bool` value but doesn’t have other, unwanted conversions, such as `bool` being promoted to `int` as part of arithmetic operations. For example, `BoolConvertible() + 5` is (unfortunately) well-formed code.