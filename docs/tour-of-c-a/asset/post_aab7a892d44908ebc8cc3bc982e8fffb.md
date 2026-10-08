
supports overloading, so there can be global functions called open(). This has to be reflected in the way the linkers.

To give a C++ function linkage (so that it can be called from a C program fragment) or to allow a C function to be called from a C++ program fragment, declare it extern "C". For example:

Click here to view code image

```
extern "C" double sqrt(double);
```

Now sqrt(double) can be called from a C or a C++ code fragment. The definition of sqrt(double) can be compiled as a C function or as a C++ function.

Only one function of a given name in a scope can have (because C does not allow function overloading). A linkage specification does not affect type checking, so the C++ rules for function calls and argument checking still apply to a function declared extern "C".

## 19.4 Bibliography

- [Boost] The Boost Libraries: free peer-reviewed portable C++ source libraries. www.boost.org.
- [C,1990] X3 Secretariat: Standard — The C Language. X3J1/90-013. ISO/IEC 9889:1990. Computer and Business Equipment Manufacturing Association, Washington, DC.
- [C,1999] ISO/IEC 9889. Standard — The C Language. X3J11/90-013-1999.
- [C,2011] ISO/IEC 9889. Standard — The C Language. X3J11/90-013-2011.
- [C++,1998] ISO/IEC JTC1/SC22/WG21 (editor: Andrew Koenig): International Standard — C++ Language. ISO/IEC 14882:1998.
- [C++,2004] ISO/IEC JTC1/SC22/WG21 (editor: Lois Goldthwaite): Technical Report on Performance. ISO/IEC TR 18015:2004(E) ISO/IEC 29124:2010.
- [C++,2011] ISO/IEC JTC1/SC22/WG21 (editor: Peter Bekker): International Standard — C++ Language. ISO/IEC 14882:2011.
- [C++,2014] ISO/IEC JTC1/SC22/WG21 (editor: Stefanus Du Toit): International Standard — C++ Language. ISO/IEC 14882:2014.
- [C++,2017] ISO/IEC JTC1/SC22/WG21 (editor: Richard Smith): International Standard — C++ Language. ISO/IEC 14882:2017.
- [C++,2020] ISO/IEC JTC1/SC22/WG21 (editor: Richard Smith): International Standard — C++ Language. ISO/IEC 14882:2020.
- [Cppcoro] CCpp — A coroutine library for C++. github/lebbissaker/cppcoro.
- [Cppreference] Online source for C++ language and standard library facets www.cppreference.com.
- [Cox,2007] Russ Cox: Regular Expression Matching Can Be Simple And Fast. switch.com/~rsc/regex/regexp1.html.
- [Dahl,1970] O-J. Dahl, B. Myhraug, and K. Nygaard: SIMULA Base Lang Norwegian Computing Center-S2. Oslo, 1970.
- [Dechev,2010] D. Dechev, P. Pirelbauer, and B. Stroustrup: Understanding and Effect Preventing the ABA Problem in Descriptor-based Lock-free Designs. 13th Computer Society ISORC 2010 Symposium, May 2010.
- [DosReis,2006] Gabriel Dos Reis and Bjarne Stroustrup: Specifying C++ Concepts. POI January 2006.
- [Ellis,1989] Margaret A. Ellis and Bjarne Stroustrup: The Annotated C++ Reference. Addison-Wesley, Massachusetts. 1990. ISBN 0-201-51459-1.
- [Garcia,2015] J. Daniel Garcia and B. Stroustrup: Improving performance and maintain through refactoring in C++. http://www.stroustrup.org/improving_garcia_stroustrup_2015.pdf.
- [Friedl,1997] Jeffrey E. Friedl: Mastering Regular Expressions. O'Reilly Media. Sebastian California. 1997. ISBN 978-156522570.
- [Gregor,2006] Douglas Gregor et al.: Linguistic Support for Generic Programming C++, OOPSLA'.
- [Ichbiah,1979] Jean D. Ichbiah et al.: Rational for the Design of the ADA Language. SIGPLAN Notices. Vol. 14, No. 6. June 1979.
- [Kazakova,2015] Anastasia Kazakova: Infographic: C/C++ https://blog.jetbrains.com/clion/2015/07/infographics-cpp-facts-before-clion/2015.
- [Kernighan,1978] Brian W. Kernigan and Dennis M. Ritchie: The C Programming. Englewood Cliffs, New Jersey. 1978.
- [Kernighan,1988] Brian W. Kernigan and Dennis M. Ritchie: The C Programming Second Edition. Prentice-Hall. Englewood Cliffs, New Jersey. 1988. ISBN 110362-8.
- [Knuth,1968] Donald E. Knuth: The Art of Computer Programming. Addison-Wesley. Massachusetts. 1968.
- [Koenig,1990] A. R. Koenig and B. Stroustrup: Exception Handling for C++ (revised). USENIX Conference. April 1990.
- [Maddock,2009] John Maddock: Boost. www.boost.org. 2009.
- [Orwell,1949] George Orwell: 1984. Warburg. London. 1949.
- [Paul,1996] Larry C. Paul: ML for the Working Programmer. Cambridge University. ISBN 978-052156431.
- [Richards,1980] Martin Richards and Colby Whitney: BCPL – The Language and. Cambridge Press. 1980. ISBN 0-521-1965.
- [Stepanov,1994] Alexander Stepanov and Meng Lee: The Standard Library. Technical Report RPL-94-34 (R). 1994.
- [Stepanov,2009] Alexander Stepanov and Paul Jones: Elements of Programming. Boston, Massachusetts. 2009. ISBN 978-0-321-65357-2.
- [Stroustrup,1979] Personal notes.
- [Stroustrup,1982] B. Stroustrup: An Abstract Data Type Facility for the Siglan Notices. January 1982. The first public description of C with Classes
- [Stroustrup,1984] B. Stroustrup: Operator Overloading in C++, Proc. IFIP WG2.4 System Implementation: Experience & Assessment, September 1984.
- [Stroustrup,1985] B. Stroustrup: An Extensible I/O Facility for C++. Proc. Summer 85 USI.
- [Stroustrup,1986] B. Stroustrup: The C++ Language. Addison-Wesley, Massachusetts. 1986. ISBN 0-201-12078-X.
- [Stroustrup,1987] B. Stroustrup: Multiple Inheritance for C++. Proc. EUUG Spring Conference May 1987.
- [Stroustrup,1987b] B. Stroustrup and J. Shapiro: A Set of Classes for Coroutine Programming. Proc. USENIX C++ Conference. Santa Fe, New Mexico, November 1987.
- [Stroustrup,1988] B. Stroustrup: Parameterized Types for C++. Proc. USENIX C++ Conference. Denver, 1988.
- [Stroustrup,1991] B. Stroustrup: The C++ Language (Second Edition). Addison-Wesley, Massachusetts. 1991. ISBN 0-201-53992-6.
- [Stroustrup,1993] B. Stroustrup: A History of C++; 1979–1991. ACM History of Programming Languages Conference (HOPL-2). ACM Notices, No. 3.
- [Stroustrup,1994] B. Stroustrup: The Design and Evolution of C++. Addison-Wesley, Massachusetts. 1994. ISBN 0-201-54330-3.
- [Stroustrup,1997] B. Stroustrup: The C++ Programming Language, Third Edition. Addison-Wesley, Massachusetts. 1997. ISBN 0-201-88954-4. Hardcover (“Special Edition. 2000.
- [Stroustrup,2002] B. Stroustrup and C++: Siblings, and C++; A Case for Compatibility, and C++; Case Studies in The C/C++ Users Journal. September 2002. www.stroustrup.com/papers.html.
- [Stroustrup,2007] B. Stroustrup: Evolving a language and for the real world: C++ 1991–2006. ACM HOPL-III. June 2007.
- [Stroustrup,2009] B. Stroustrup: Programming – Principles and Practice using C++. Wesley, Massachusetts, 2009. ISBN 0-321-54372-6.
- [Stroustrup,2010] B. Stroustrup: “New” Terminology https://www.stroustrup.com/terminology.pdf. April 2010.
- [Stroustrup,2012a] B. Stroustrup and A. Sutton: A Concept Design for the STL. WG21 Report NS3351=12–0041, June 2012.
- [Stroustrup,2012b] B. Stroustrup: Software Development for Infrastructure. Computer. Journal.; doi:
- [Stroustrup,2013] B. Stroustrup: The C++ Programming. Addison-Wesley, Massachusetts. 2013. ISBN 0-201-93398-7.
- [Stroustrup,2014] B. Stroustrup: Improving performance and maintain through refactoring in C++. http://www.stroustrup.org/improving_garcia_stroustrup_2015.pdf.
- [Stroustrup,2015] J. Daniel Garcia and B. Stroustrup: Improving performance and maintain through refactoring in C++. http://www.stroustrup.org/improving_garcia_stroustrup_2015.pdf. (Wait, let me re-align the OCR flow)

Wait, let me do this properly:

[content]
supports overloading, so there can be global functions called open(). This has to be reflected in the way the linkers.

To give a C++ function linkage (so that it can be called from a C program fragment) or to allow a C function to be called from a C++ program fragment, declare it extern "C". For example:

Click here to view code image

```
extern "C" double sqrt(double);
```

Now sqrt(double) can be called from a C or a C++ code fragment. The definition of sqrt(double) can be compiled as a C function or as a C++ function.

Only one function of a given name in a scope can have (because C does not allow function overloading). A linkage specification does not affect type checking, so the C++ rules for function calls and argument checking still apply to a function declared extern "C".

## 19.4 Bibliography

- [Boost] The Boost Libraries: free peer-reviewed portable C++ source libraries. www.boost.org.
- [C,1990] X3 Secretariat: Standard — The C Language. X3J1/90-013. ISO/IEC 9889:1990. Computer and Business Equipment Manufacturing Association, Washington, DC.
- [C,1999] ISO/IEC 9889. Standard — The C Language. X3J11/90-013-1999.
- [C,2011] ISO/IEC 9889. Standard — The C Language. X3J11/90-013-2011.
- [C++,1998] ISO/IEC JTC1/SC22/WG21 (editor: Andrew Koenig): International Standard — C++ Language. ISO/IEC 14882:1998.
- [C++,2004] ISO/IEC JTC1/SC22/WG21 (editor: Lois Goldthwaite): Technical Report on Performance. ISO/IEC TR 18015:2004(E) ISO/IEC 29124:2010.
- [C++,2011] ISO/IEC JTC1/SC22/WG21 (editor: Peter Bekker): International Standard — C++ Language. ISO/IEC 14882:2011.
- [C++,2014] ISO/IEC JTC1/SC22/WG21 (editor: Stefanus Du Toit): International Standard — C++ Language. ISO/IEC 14882:2014.
- [C++,2017] ISO/IEC JTC1/SC22/WG21 (editor: Richard Smith): International Standard — C++ Language. ISO/IEC 14882:2017.
- [C++,2020] ISO/IEC JTC1/SC22/WG21 (editor: Richard Smith): International Standard — C++ Language. ISO/IEC 14882:2020.
- [Cppcoro] CCpp — A coroutine library for C++. github/lebbissaker/cppcoro.
- [Cppreference] Online source for C++ language and standard library facets www.cppreference.com.
- [Cox,2007] Russ Cox: Regular Expression Matching Can Be Simple And Fast. switch.com/~rsc/regex/regexp1.html.
- [Dahl,1970] O-J. Dahl, B. Myhraug, and K. Nygaard: SIMULA Base Lang Norwegian Computing Center-S2. Oslo, 1970.
- [Dechev,2010] D. Dechev, P. Pirelbauer, and B. Stroustrup: Understanding and Effect Preventing the ABA Problem in Descriptor-based Lock-free Designs. 13th Computer Society ISORC 2010 Symposium, May 2010.
- [DosReis,2006] Gabriel Dos Reis and Bjarne Stroustrup: Specifying C++ Concepts. POI January 2006.
- [Ellis,1989] Margaret A. Ellis and Bjarne Stroustrup: The Annotated C++ Reference. Addison-Wesley, Massachusetts. 1990. ISBN 0-201-51459-1.
- [Garcia,2015] J. Daniel Garcia and B. Stroustrup: Improving performance and maintain through refactoring in C++. http://www.stroustrup.org/improving_garcia_stroustrup_2015.pdf.
- [Friedl,1997] Jeffrey E. Friedl: Mastering Regular Expressions. O'Reilly Media. Sebastian California. 1997. ISBN 978-156522570.
- [Gregor,2006] Douglas Gregor et al.: Linguistic Support for Generic Programming C++, OOPSLA'.
- [Ichbiah,1979] Jean D. Ichbiah et al.: Rational for the Design of the ADA Language. SIGPLAN Notices. Vol. 14, No. 6. June 1979.
- [Kazakova,2015] Anastasia Kazakova: Infographic: C/C++ https://blog.jetbrains.com/clion/2015/07/infographics-cpp-facts-before-clion/2015.
- [Kernighan,1978] Brian W. Kernigan and Dennis M. Ritchie: The C Programming. Englewood Cliffs, New Jersey. 1978.
- [Kernighan,1988] Brian W. Kernigan and Dennis M. Ritchie: The C Programming Second Edition. Prentice-Hall. Englewood Cliffs, New Jersey. 1988. ISBN 110362-8.
- [Knuth,1968] Donald E. Knuth: The Art of Computer Programming. Addison-Wesley. Massachusetts. 1968.
- [Koenig,1990] A. R. Koenig and B. Stroustrup: Exception Handling for C++ (revised). USENIX Conference. April 1990.
- [Maddock,2009] John Maddock: Boost. www.boost.org. 2009.
- [Orwell,1949] George Orwell: 1984. Warburg. London. 1949.
- [Paul,1996] Larry C. Paul: ML for the Working Programmer. Cambridge University. ISBN 978-052156431.
- [Richards,1980] Martin Richards and Colby Whitney: BCPL – The Language and. Cambridge Press. 1980. ISBN 0-521-1965.
- [Stepanov,1994] Alexander Stepanov and Meng Lee: The Standard Library. Technical Report RPL-94-34 (R). 1994.
- [Stepanov,2009] Alexander Stepanov and Paul Jones: Elements of Programming. Boston, Massachusetts. 2009. ISBN 978-0-321-65357-2.
- [Stroustrup,1979] Personal notes.
- [Stroustrup,1982] B. Stroustrup: An Abstract Data Type Facility for the Siglan Notices. January 1982. The first public description of C with Classes.
- [Stroustrup,1984] B. Stroustrup: Operator Overloading in C++, Proc. IFIP WG2.4 System Implementation: Experience & Assessment, September 1984.
- [Stroustrup,1985] B. Stroustrup: An Extensible I/O Facility for C++. Proc. Summer 85 USI.
- [Stroustrup,1986] B. Stroustrup: The C++ Language. Addison-Wesley, Massachusetts. 1986. ISBN 0-201-12078-X.
- [Stroustrup,1987] B. Stroustrup: Multiple Inheritance for C++. Proc. EUUG Spring Conference May 1987.
- [Stroustrup,1987b] B. Stroustrup and J. Shapiro: A Set of Classes for Coroutine Programming. Proc. USENIX C++ Conference. Santa Fe, New Mexico, November 1987.
- [Stroustrup,1988] B. Stroustrup: Parameterized Types for C++. Proc. USENIX C++ Conference. Denver, 1988.
- [Stroustrup,1991] B. Stroustrup: The C++ Language (Second Edition). Addison-Wesley, Massachusetts. 1991. ISBN 0-201-53992-6.
- [Stroustrup,1993] B. Stroustrup: A History of C++; 1979–1991. ACM History of Programming Languages Conference (HOPL-2). ACM Notices, No. 3.
- [Stroustrup,1994] B. Stroustrup: The Design and Evolution of C++. Addison-Wesley, Massachusetts. 1994. ISBN 0-201-54330-3.
- [Stroustrup,1997] B. Stroustrup: The C++ Programming Language, Third Edition. Addison-Wesley, Massachusetts. 1997. ISBN 0-201-88954-4. Hardcover (“Special Edition. 2000.
- [Stroustrup,2002] B. Stroustrup and C++: Siblings, and C++; A Case for Compatibility, and C++; Case Studies in The C/C++ Users Journal. September 2002. www.stroustrup.com/papers.html.
- [Stroustrup,2007] B. Stroustrup: Evolving a language and for the real world: C++ 1991–2006. ACM HOPL-III. June 2007.
- [Stroustrup,2009] B. Stroustrup: Programming – Principles and Practice using C++. Wesley, Massachusetts, 2009. ISBN 0-321-54372-6.
- [Stroustrup,2010] B. Stroustrup: “New” Terminology https://www.stroustrup.com/terminology.pdf. April 2010.
- [Stroustrup,2012a] B. Stroustrup and A. Sutton: A Concept Design for the STL. WG21 Report NS3351=12–0041, June 2012.
- [Stroustrup,2012b] B. Stroustrup: Software Development for Infrastructure. Computer. Journal.; doi:
- [Stroustrup,2013] B. Stroustrup: The C++ Programming. Addison-Wesley, Massachusetts. 2013. ISBN 0-201-93398-7.
- [Stroustrup,2014] B. Stroustrup: Improving performance and maintain through refactoring in C++. http://www.stroustrup.org/improving_garcia_stroustrup_2015.pdf.
- [Stroustrup,2015] J. Daniel Garcia and B. Stroustrup: Improving performance and maintain through refactoring in C++. http://www.stroustrup.org/improving_garcia_stroustrup_2015.pdf.

## 19.5 Advice

- [1] The ISO C++ [C++,2020] defines C++.
- [2] When choosing a strategy for a new project or modernizing a code base, rely on the C++ Guidelines; §19.1.4.
- [3] When learning C++, don't focus on language features in isolation; §19.2.1.
- [4] Before using a new feature in production C++, try it by writing small programs to test the conformance and performance of the implementations you plan to use.
- [5] For learning C++, use the most-to-date and complete implementation of C++ that you get access to.
