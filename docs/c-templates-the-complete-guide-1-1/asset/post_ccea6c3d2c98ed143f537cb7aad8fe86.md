
If you find that the repeated qualifications are cluttering up your code, you can combine them into a name for the dependent base class discussed next and call it.

```cpp
// Version 2
template<typename T>
class D2 : public B2<T> {
public:
  using Base = B2<T>;                   // @1 dependent name now
                                        //   in scope
  void f1() { Base::f1(); }             // @2 f1
};
```

The key point at @2 succeeds and finds the existing declaration of f1. However, using declaration is not verified until instantiation time and so no error is detected. There are some subtle implications to this design. Note in particular that the lookup for the name Base<T>::f1 happens at parse time only, which means early errors can occur if the derived class member is not accessible.

When searching for a qualified name within the current instantiation, the compiler first looks for a member in the current instantiation and its partial instantiations, then searches in the set of its template's template argument list. If it finds a member, then the qualified name refers to a member of the current instantiation and will not be a dependent name. This also explains that it must be a dependent name if the qualified name refers to a member of an unknown specialization.

```cpp
class NonDep {
public:
  using Type = int;
};

template<typename T>
class Dep {
public:
  using OtherType = T;
};

template<typename T>
class Dep2 : public NonDep, public Dep<T> {
public:
  void f1() {
    typename Dep2::Type x;              // Error: NonDep::Type is
                                        // not found
    typename Dep2::OtherType y;        // Error: ambiguous? no
                                        // unknown specialization
  }
};
```

## 13.5 Afternotes

The first template really is pure template declarations and was developed by a colleague as part of a decade-long project to demonstrate how the compiler's diagnostic messages and error messages can be improved.

After that, the compiler developed a sophisticated algorithm to avoid repetitive template instantiation. The algorithm works by reading a source file and creating a list of the template arguments. If a particular template specialization was already instantiated, the compiler can reuse it. This is especially helpful for a library like STL, where many templates are instantiated with the same arguments. This optimization is called memoization, and it is the key to the performance of the compiler.

Bill Gibbons was Taligent's representative on the C++ committee and was the principal advocate for making templates unambiguous. The proposal was known as "The Taligent Design (D&D)" (the PDF linked here) as proposed by Hubert Ficker (IBM). It became a C++ compiler. Among its competitors, the C++ compiler was equally recognized for its high quality diagnostics. The fact that template diagnostics were not always displayed with instantiation info unnecessarily contributed to this perception.

Relatively early during the development of templates, Tom Pennello—a talented friend and colleague at Edison Design Group—was among those who proposed a standard solution for the problem. It is based on the notion that all dependent names should be looked up at definition time. Furthermore, other properties (e.g., whether the name refers to a type, a template, or a function) should also be determined at definition time. This was especially important for implementing overload resolution and type deduction.

This work on the semantics of dependent names became known as the "two-phase lookup" and was adopted by the C++ standardization committee. It was also the basis for the "export" keyword, which was later removed from the language. The "export" keyword was intended to allow separate compilation of templates, but it was not widely implemented and was eventually removed.

Name is still not found, a hard error is issued and compilation fails. However, if the name is found in a dependent base, a warning is issued, and the name is marked to be treated as if it were dependent, so that lookup will be reattempted at instantiation time.

The lookup rule that causes a name in a nondependent base to hide an identically named template parameter (Section 14.6.2.1 on page 239) is an oversight, but suggestions to change the rule have not garnered support from the C++ standardization committee. It is best to deal with template parameter names that are also used in nondependent base classes. Good naming conventions are helpful for such problems.

Friend name injection was considered harmful because it made the validity of programs more sensitive to the ordering of instantiations. Bill Gibbons (who at the time was working on the Taligent compiler) was among the most vocal supporters of addressing the problem, because eliminating instantiation order dependence enabled new and interesting C++ development environments (on which Taligent was rumored to be working). However, the Barton-Nackman trick (Section 21.3.1 on page 697) required a form of friend name injection, and it is this particular technique that caused it to remain in the language in its current weak-but-friend-based API.

Andrew Koenig first proposed ADL for operator functions only (which is why ADL is sometimes called Koenig lookup). The motivation was primarily aesthetics: Explicitly qualifying operator names with their own namespace looks awkward at best (e.g., instead of `a+b` we may need to write: `operator+(a, b)`, and having to write using declarations for every operator can lead to unwieldy code). Hence, it was decided that operators would be looked up in the namespaces associated with arguments. This later extended to ordinary function names to accommodate a limited kind of friend name injection and to support a two-phase lookup model for templates and their instantiation (Chapter 14). The generalized ADL rules are also called extended Koenig lookup.

The specification for the angle bracket hack was added to C++11 by David Vandevoorde through his paper N1757. He also added the digraph hack to the resolution of Core issue 1470, to address a request of the United States' review of a draft of the C++11 standard.

- 1. In C++98/C++03, this was called Koenig lookup (or extended Koenig lookup) after Andrew Koenig, who first proposed a variation of this mechanism.
- 2. Although this was clearly intended by those who wrote the C++ standard, it is not clearly spelled out in the standard.
- 3. Note the odd punctuation in the above parsing. `<>` is a cast operation—not another source of syntactic ambiguity.
- 4. Specific operations were introduced to address initialization issues described in this section.
- 5. The 1998 version of the C++ standard did not support this “angle bracket hack.” However, the need to introduce a space between the two consecutive right angle brackets was such a common stumbling block for beginning template users that the committee decided to codify this hack in the C++11 standard.
- 6. Some compilers that provide a C++98 or C++03 mode keep the C++11 behavior in those modes and thus print `0` even when formally compiling C++98 or C++03 code.
- 7. This is therefore an exception to the aforementioned maxim that much principle.
- 8. Thanks to Richard Smith for pointing that out.
- 9. Note that C++20 will probably remove the need for `typename` in most cases (see Section 17.1.1 on page 354 for details).
- 10. Syntactically, only type names are permitted within these contexts, as clarified more precisely above.
- 11. Adapted from [VandevoordeSaks09], proving once and for all that C++ promotes code reuse.
- 12. The terms type-dependent expression and value-dependent expression are used in the C++ standard to describe the semantics of templates, and have an important role in several aspects of templates (Chapter 14). On the other hand, the term instantiation-dependent expression is mainly only used by the authors of C++ compilers. Our definition of an instantiation-dependent expression differs from the definition in the C++ standard, which provides the basis for binary interoperability among a number of different C++ compilers.
- 13. This is part of the two-phase lookup rules that distinguish between a first phase when template definitions are first seen and a second phase when templates are instantiated (see Section 14.3.2 on page 349).
- 14. However, the lookup is nonetheless repeated when the template is instantiated, and if a different result is produced in that context, the program is ill-formed.
- 15. Braces are not entirely without problems either. Specifically, the syntax for specialized class templates would require nontrivial adaptation.
- 16. Fortunately, they found out before they released the new functionality.
- 17. Ironically, the first of these implementations had been developed by HP as well.
