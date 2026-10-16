At this stage in its development, the language included dynamic binding, function and operator overloading, and improved type-checking, but not type parameters, exceptions, or multiple inheritance. These would all come later.

# 2.6.2 C++: Growth

In late 1985, Stroustrup published the first edition of his book on C++. In the meantime, Cpre and Cfront had already been distributed for educational purposes essentially at no cost, and interest in the language had begun to grow in industry. Thus, a first commercial implementation was made available in 1986.

In 1987, the first conference specifically on C++ was organized by USENIX (the UNIX users’ association). By October 1988, Stroustrup estimates that there were about 15,000 users of the language, with PC versions of C++ compilers appearing that same year. Between October 1979, when Stroustrup first began using Cpre himself and October 1991, Stroustrup estimates that the number of C++ users doubled every seven and a half months. The success of the language indicated to Stroustrup and others that a concerted attempt at creating a standard language definition was necessary, including possible extensions that had not yet been implemented.

# 2.6.3 C++: Standardization

Because C++ was rapidly growing in use, was continuing to evolve, and had a number of different implementations, the standardization presented a problem. Moreover, because of the growing user pool, there was some pressure to undertake and complete the effort as quickly as possible. At the same time, Stroustrup felt that the evolution of the language was not yet complete and should be given some more time.

Nevertheless, Stroustrup produced a reference manual in 1989 (the *Annotated Reference Manual*, or *ARM*; Ellis and Stroustrup [1990]) that included all of C++ up to that point, including proposals for new exception-handling and template (type parameter) mechanisms (multiple inheritance had already been added to the language and Cfront that same year). In 1990 and 1991, respectively, ANSI and ISO standards committees were convened; these soon combined their efforts and accepted the ARM as the “base document” for the standardization effort.

Then began a long process of clarifying the existing language, producing precise descriptions of its features, and adding features and mechanisms (mostly of a minor nature after the *ARM*) whose utility was agreed upon. In 1994, a major development was the addition of a standard library of containers and algorithms (the Standard Template Library, or STL). The standards committees produced two drafts of proposed standards in April 1995 and October 1996 before adopting a proposed standard in November 1997. This proposal became the actual ANSI/ISO standard in August 1998.

# 2.6.4 C++: Retrospective

Why was C++ such a success? First of all, it came on the scene just as interest in object-oriented techniques was exploding. Its straightforward syntax, based on C, was tied to no particular operating environment. The semantics of C++ incurred no performance penalty. These qualities allowed C++ to bring object-oriented features into the mainstream of computing. The popularity of C++ was also enhanced by its flexibility, its hybrid nature, and the willingness of its designer to extend its features based on practical experience. (Stroustrup lists Algol68, CLU, Ada, and ML as major influences after C and Simula67).