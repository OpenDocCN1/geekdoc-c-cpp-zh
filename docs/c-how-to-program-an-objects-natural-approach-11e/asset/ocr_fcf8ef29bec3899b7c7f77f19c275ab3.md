Google’s C++ Style Guide says to “avoid complicated template programming.”^10 Similarly, the C++ Core Guidelines indicate that you should “use template metaprogramming only when you really need to” and that it’s “hard to get right, … and is often very hard to maintain.”^11 These guidelines could be updated when developers gain more experience using C++20 Concepts and future C++ enhancements.

# # 15.2 Custom Class Templates and Compile-Time Polymorphism

A template enables compile-time (or static) polymorphism^12,13 by specifying capabilities generically, then letting the compiler instantiate the template, generating type-specific code specializations on demand. Class templates are called parameterized types because they require one or more parameters to tell the compiler how to customize a class template to form a class-template specialization from which objects can be instantiated. You write one class-template definition. When you need particular specializations, you use concise, simple notations to instantiate the template. Then, the compiler writes only those specializations for you. One Stack class template, for example, could become the basis for creating many class-template specializations, such as “Stack of doubles,” “Stack of ints,” “Stack of Employees,” “Stack of Bills” or “Stack of ActivationRecords.”

To use a type with a template, the type must meet the template’s requirements. For example, a template might require objects of a specified type to

+   - be initializable with a default constructor,
+   - be copyable or movable,
+   - be comparable with operator < to determine their sort order,
+   - have specific member functions and more.

Compilation errors usually occur when you instantiate a template with a type that does not meet the template’s requirements.

# ## Creating Class Template Stack&lt;T&gt;

Let’s jump into coding a custom Stack class template. It’s possible to understand the notion of a stack independently of the kinds of items you place onto or remove from it. A stack is simply a last-in, first-out (LIFO) data structure. Class templates encourage software reuse by enabling the compiler to instantiate many type-specific class-template specializations from a single class template—as you saw with the stack container adaptor in Section 13.12.1. Here (Fig. 15.1), we define a stack generically, then instantiate and

+   10. “Google C++ Style Guide—Template Metaprogramming.” Accessed April 18, 2023. https://google.github.io/styleguide/cppguide.html#Template_metaprogramming.
+   11. “C++ Core Guidelines, T.120: Use Template Metaprogramming Only When You Really Need To.” Accessed April 18, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rt-metameta.
+   12. “C++—Static Polymorphism.” Wikipedia. Wikimedia Foundation. Accessed April 18, 2023. https://en.wikipedia.org/wiki/C%2B%2B#Static_polymorphism.
+   13. Kateryna Bondarenko, “Static Polymorphism in C++,” May 6, 2019. Accessed April 18, 2023. https://medium.com/@kateolena/static-polymorphism-in-c-9e1ae27a945b.