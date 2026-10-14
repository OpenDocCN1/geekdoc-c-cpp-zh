
- The C# Programming Guide describes ref returns and ref locals at https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/ref-returns.
- Although ref returns and ref locals weren’t introduced until C# v7.0, the idea has been around much longer, as Eric Lippert explains at https://ericlippert.com/2011/06/23/ref-returns-and-ref-locals/.
- Vladimir Sadov examines the rules around whether a ref local is safe to return at http://mustoverride.com/safe-to-return/.
- The operation of the garbage collector is a complex topic, but a good starting point is the Microsoft documentation at https://docs.microsoft.com/en-us/dotnet/standard/garbage-collection/fundamentals.
- Andrew Hunter also describes garbage collection in his blog at https://www.red-gate.com/simple-talk/development/dotnet-development/understanding-garbage-collection-in-net/.
- The Microsoft documentation on value tuple support from C# v7.0 onward is at https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/value-tuples.

## Chapter 4

- Eric Lippert has written extensively about value types and touches on modifying returned values at https://ericlippert.com/2008/05/14/mutating-readonly-structs/.
- Lippert examines the construction of value types and the use of an intermediate temporary instance in this post: https://ericlippert.com/2010/10/11/debunking-another-myth-about-value-types/.
- The C# Language Specification on object creation can be read online at https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/expressions#117152-object-creation-expressions. Object initializers are covered at https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/expressions#117153-object-initializers.
- The Microsoft documentation on casts, including a link to user-defined conversion methods, is at https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/types/casting-and-type-conversions#implicit-conversions.
- Jon Skeet investigates read-only fields in his blog at https://codeblog.jonskeet.uk/2014/07/16/micro-optimization-the-surprising-inefficiency-of-readonly-fields/.
- The Microsoft documentation for in parameters (https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/in-parameter-modifier) and ref readonly return values and locals (https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/ref#reference-return-values) has good information on the caveats and rules for correctly using them.
- Sergey Tepliakov’s blog has some enlightening articles on in and ref readonly performance too, at https://devblogs.microsoft.com/premier-developer/the-in-modifier-and-the-readonly-structs-in-c/ and https://devblogs.microsoft.com/premier-developer/performance-traps-of-ref-locals-and-ref-returns-in-c/.

## Chapter 5

- The quote from Donald Knuth is from his ACM Turing Award lecture in 1974. He went on to say—much more famously—that “premature optimization is the root of all evil.” The full text is available at https://dl.acm.org/doi/10.1145/1283920.1283929.
- Eric Lippert’s blog post on the subject of null is enlightening: https://ericlippert.com/2013/07/25/what-is-the-type-of-the-null-literal/.
- String interning is documented by Microsoft at https://docs.microsoft.com/en-us/dotnet/api/system.string.intern?view=net-5.0.
- A variety of articles address floating-point representation and the pitfalls that can arise. Frances Buontempo gives an overview with examples and further references for those who want to dig deeper in her Overload article “Floating Point Fun and Frolics” at https://accu.org/journals/overload/17/91/buontempo_1558.
- Richard Harris has written extensively about floating-point comparisons and arithmetic. This series of Overload articles examines the common alternatives to IEEE-754 floating-point:
    - “You’re Going To Have To Think!,” https://accu.org/journals/overload/18/99/harris_1702
    - “Why Fixed Point Won’t Cure Your Floating Point Blues,” https://accu.org/journals/overload/18/100/harris_1717
    - “Why Rationals Won’t Cure Your Floating Point Blues,” https://accu.org/journals/overload/19/101/harris_1986
    - “Why Computer Algebra Won’t Cure Your Floating Point Blues,” https://accu.org/journals/overload/19/102/harris_1979
    - “Why Interval Arithmetic Won’t Cure Your Floating Point Blues,” https://accu.org/journals/overload/19/103/harris_1974
- A comparison of C#’s floating-point types can be found in the Microsoft documentation at https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/types#floating-point-types.
- The Microsoft documentation gives an overview of the constant pattern at https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/patterns#constant-pattern.
- The declaration pattern is described in the Microsoft documentation at https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/patterns#declaration-and-type-patterns.
- Nullable value type operator overloads are described in the C# Language Specification, which has a short remark about operator==, at https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/nullable-value-types#lifted-operators.
- The C# Language Specification also has a section on nullable reference types at https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/nullable-reference-types.
- Lippert has a great series of blogs about nullable value types starting here: https://ericlippert.com/2012/12/20/nullable-micro-optimizations-part-one/.
- Lippert examines the concept of lifted operators at https://docs.microsoft.com/en-us/archive/blogs/ericlippert/what-exactly-does-lifted-mean.
- MSDN Magazine looks at why value tuples aren’t immutable at https://docs.microsoft.com/en-us/archive/msdn-magazine/2018/june/csharp-tuple-trouble-why-csharp-tuples-get-to-break-the-guidelines.

## Chapter 6

- For an in-depth look at value types in modeling complex systems, see Dirk Bäumer et al., “Values in Object Systems,” Ubilab Technical Report, https://riehle.org/computer-science/research/1998/ubilab-tr-1998-10-1.pdf.
- Kevlin Henney covers the taxonomy of object types and offers other valuable insights regarding object comparisons in C++ and C# at https://www.slideshare.net/Kevlin/objects-of-value.
- Martin Fowler describes the anemic domain model at https://www.martinfowler.com/bliki/AnemicDomainModel.html.
- Fowler describes aliasing an object causing bugs at https://www.martinfowler.com/bliki/AliasingBug.html.
- Aliasing is not a new idea, either, as you can see in Eric S. Raymond’s The Jargon File: http://www.catb.org/jargon/html/A/aliasing-bug.html.
- Scott Stanchfield’s article on the perils of using a language that has no concept of pass-by value is quite old and focused on the Java of the era, but still enlightening: http://www.javaduude.com/articles/passbyvalue.htm.
- The contract for IComparable implementations is described in the Microsoft documentation at https://docs.microsoft.com/en-us/dotnet/api/system.icomparable-1.compareto?view=net-5.0#notes-to-implementers.
- Henney looks at some patterns for value types, including symmetry, in this conference paper: https://www.researchgate.net/publication/244405850_The_Good_the_Bad_and_the_Koyaanisqatsi_Consideration_of_Some_Patterns_for_Value_Objects.
- Scott Meyers wrote seminal books that will be recognized instantly by C++ programmers everywhere, but he has much to say that’s relevant to programmers in any language. In particular, Effective C++, 3rd edition (Addison-Wesley, 2005), and More Effective C++ (Addison-Wesley, 1996) look at making interfaces easy to use correctly and hard to use incorrectly, as well as the benefits of moving functions outside of the class.
- Intransitive or non-transitive dice are a fun way to explore and challenge the idea of less-than and intrinsic ordering; see the Rosetta Code site at https://rosettacode.org/wiki/Non-transitive_dice.
