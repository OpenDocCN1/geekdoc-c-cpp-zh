Instead of using `Type = C` we use using `Type = M`.

¹¹ As mentioned elsewhere, treating a parameter of value reference type as a value rather than an alias is intended as a safety feature, because anything with a name (like a parameter) can easily be referenced multiple times in a function. If we are in an rvalue, its first use might cause its value to be “moved away,” causing surprising behavior for every subsequent use. See Section 6.1 on page 25 and Section 15.3 on page 280.

¹² When we used the latter formulation in our introductory example of use, we implicitly assumed that the iterators produced references to some underlying storage. While this is generally true for container iterators (and required by the standard for containers other than `vector<bool>`), it is not the case for all iterators.

¹³ This example does not use our usual style for placing the `*` immediately adjacent to the `auto` keyword, because it could mislead the reader into thinking we are declaring two pointers. On the other hand, the opacity of the dereference function is a good argument for being conservative when declaring multiple variables in a single declaration.

¹⁴ The term structured bindings was used in the original proposal for the feature and was also eventually used for the formal specification in the language. Briefly, however, that specification used the term decomposition declarations instead.

¹⁵ The other two places where built-in arrays are copied are lambda captures and generated copy constructors.

¹⁶ This translation model of lambdas is actually used in the specification of the C++ language, making it both a convenient and an accurate description of the semantics. Captured variables become data members, the conversion of a noncapturing lambda to a function pointer is modeled as a conversion function in the class, and so on. And because lambdas are function objects, whenever we declare functor objects instead, they also apply to lambdas.

¹⁷ Note the distinction between a placeholder type, which is `auto` or `decltype(auto)`, and can resolve to any kind of type, and a placeholder class type, which is a template name and can only resolve to a class type that is an instance of the indicated template.

¹⁸ As with ordinary function template deduction, SFINAE could apply if, for example, substituting the deduced arguments in the guided type failed. That is not the case in this simple example.

¹⁹ Chapter 8 introduces the ability to “specialize” class templates in various ways. Such specializations do not participate in class template argument deduction.