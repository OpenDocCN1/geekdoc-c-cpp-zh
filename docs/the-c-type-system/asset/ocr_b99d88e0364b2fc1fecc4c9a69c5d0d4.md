+   - The C# Language Specification also has a section on nullable reference types at https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/nullable-reference-types.
+   - Lippert has a great series of blogs about nullable value types starting here: https://ericlippert.com/2012/12/20/nullable-micro-optimizations-part-one/.
+   - Lippert examines the concept of lifted operators at https://docs.microsoft.com/en-us/archive/blogs/ericlippert/what-exactly-does-lifted-mean.
+   - MSDN Magazine looks at why value tuples aren’t immutable at https://docs.microsoft.com/en-us/archive/msdn-magazine/2018/june/csharp-tuple-trouble-why-csharp-tuples-get-to-break-the-guidelines.

# Chapter 6

+   - For an in-depth look at value types in modeling complex systems, see Dirk Bäumer et al., “Values in Object Systems,” Ubilab Technical Report, https://riehle.org/computer-science/research/1998/ubilab-tr-1998-10-1.pdf.
+   - Kevlin Henney covers the taxonomy of object types and offers other valuable insights regarding object comparisons in C++ and C# at https://www.slideshare.net/Kevlin/objects-of-value.
+   - Martin Fowler describes the anemic domain model at https://www.martinfowler.com/bliki/AnemicDomainModel.html.
+   - Fowler describes aliasing an object causing bugs at https://www.martinfowler.com/bliki/AliasingBug.html.
+   - Aliasing is not a new idea, either, as you can see in Eric S. Raymond’s The Jargon File: http://www.catb.org/jargon/html/A/aliasing-bug.html.
+   - Scott Stanchfield’s article on the perils of using a language that has no concept of pass-by value is quite old and focused on the Java of the era, but still enlightening: http://www.javaduude.com/articles/passbyvalue.htm.
+   - The contract for IComparable implementations is described in the Microsoft documentation at https://docs.microsoft.com/en-us/dotnet/api/system.icomparable-1.compareto?view=net-5.0#notes-to-implementers.
+   - Henney looks at some patterns for value types, including symmetry, in this conference paper: https://www.researchgate.net/publication/244405850_The_Good_the_Bad_and_the_Koyaanisqatsi_Consideration_of_Some_Patterns_for_Value_Objects.
+   - Scott Meyers wrote seminal books that will be recognized instantly by C++ programmers everywhere, but he has much to say that’s relevant to programmers in any language. In particular, Effective C++, 3rd edition (Addison-Wesley, 2005), and More Effective C++ (Addison-Wesley, 1996) look at making interfaces easy to use correctly and hard to use incorrectly, as well as the benefits of moving functions outside of the class.
+   - Intransitive or non-transitive dice are a fun way to explore and challenge the idea of less-than and intrinsic ordering; see the Rosetta Code site at https://rosettacode.org/wiki/Non-transitive_dice.