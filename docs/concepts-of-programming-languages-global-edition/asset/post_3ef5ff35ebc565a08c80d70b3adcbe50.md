
## 2.20.1 XSLT

eXtensible markup language (XML) is a metamarkup language. Such a language is used to define markup languages. XML-derived markup languages are used to define XML data documents. Although XML documents are human readable, they are processed by computers. This processing sometimes consists only of transformations to alternative forms that can be effectively displayed or printed. In many cases, such transformations are to HTML, which can be displayed by a Web browser. In other cases, the data in the document is processed, just as with other forms of data files.

The transformation of XML documents to HTML documents is specified in another markup language, eXtensible stylesheet language transformations (XSLT) (www.w3.org/TR/XSLT). XSLT can specify programming-like operations. Therefore, XSLT is a markup-programming hybrid language. XSLT was defined by the World Wide Web Consortium (W3C) in the late 1990s.

An XSLT processor is a program that takes as input an XML data document and an XSLT document (which is also in the form of an XML document). In this processing, the XML data document is transformed to another XML document, using the transformations described in the XSLT document. The XSLT document specifies transformations by defining templates, which are data patterns that could be found by the XSLT processor in the XML input file. Associated with each template in the XSLT document are its transformation instructions, which specify how the matching data is to be transformed before being put in the output document. So, the templates (and their associated processing) act as subprograms, which are “executed” when the XSLT processor finds a pattern match in the data of the XML document.

XSLT also has programming constructs at a lower level. For example, a looping construct is included, which allows repeated parts of the XML document to be selected. There is also a sort process. These lower-level constructs are specified with XSLT tags, such as <for-each>.

21. The output document of the XSLT processor could also be in HTML or plain text.

## 2.20.2 JSP

The “core” part of the Java Server Pages Standard Tag Library (JSTL) is another markup-programming hybrid language, although its form and purpose are different from those of XSLT. Before discussing JSTL, it is necessary to introduce the ideas of servlets and Java Server Pages (JSP). A servlet is an instance of a Java class that resides on and is executed on a Web server system. The execution of a servlet is requested by a markup document being displayed by a Web browser. The servlet’s output, which is in the form of an HTML document, is returned to the requesting browser. A program that runs in the Web server process, called a servlet container, controls the execution of servlets. Servlets are commonly used for form processing and for database access.

JSP is a collection of technologies designed to support dynamic Web documents and provide other processing needs of Web documents. When a JSP document, which is often a mixture of HTML and Java, is requested by a browser, the JSP processor program, which resides on a Web server system, converts the document to a servlet. The document's embedded Java code is copied to the servlet. The plain HTML is copied into Java print statements that output it as is. The JSTL markup in the JSP document is processed, as discussed in the following paragraph. The servlet produced by the JSP processor is run by the servlet container.

The JSTL defines a collection of XML action elements that control the processing of the JSP document on the Web server. These elements have the same form as other elements of HTML and XML. One of the most commonly used JSTL control action elements is if, which specifies a Boolean expression as an attribute.22 The content of the if element (the text between the opening tag (<if>) and its closing tag (</if>)) is HTML code that will be included in the output document only if the Boolean expression evaluates to true. The if element is related to the C/C++ #if preprocessor command. The JSP container processes the JSTL parts of JSP documents in a way that is similar to how the C/C++ preprocessor processes C and C++ programs. The preprocessor commands are instructions for the preprocessor to specify how the output file is to be constructed from the input file. Similarly, JSTL control action elements are instructions for the JSP processor to specify how to build the XML output file from the XML input file.

One common use of the if element is for the validation of form data submitted by a browser user. Form data is accessible by the JSP processor and can be tested with the if element to ensure that it is sensible data. If not, the if element can insert an error message for the user in the output document.

For multiple selection control, JSTL has choose, when, and otherwise elements. JSTL also includes a forEach element, which iterates over collections, which typically are form values from a client. The forEach element can include begin, end, and step attributes to control its iterations.

## SUMMARY

We have investigated the development of a number of programming languages. This chapter gives the reader a good perspective on current issues in language design. We have set the stage for an in-depth discussion of the important features of contemporary languages.

## BIBLIOGRAPHIC NOTES

Perhaps the most important source of historical information about the development of early programming languages is History of Programming Languages, edited by Richard Wexelblat (1981). It contains the developmental background

and environment of 13 important programming languages, as told by the designers themselves. A similar work resulted from a second “history” conference, published as a special issue of ACM SIGPLAN Notices (ACM, 1993a). In this work, the history and evolution of 13 more programming languages are discussed.

The paper “Early Development of Programming Languages” (Knuth and Pardo, 1977), which is part of the Encyclopedia of Computer Science and Technology, is an excellent 85-page work that details the development of languages up to and including Fortran. The paper includes example programs to demonstrate the features of many of those languages.

Another book of great interest is Programming Languages: History and Fundamentals, by Jean Sammet (1969). It is a 785-page work filled with details of 80 programming languages of the 1950s and 1960s. Sammet has also published several updates to her book, such as Roster of Programming Languages for 1974–75 (1976).

22. An attribute in HTML, which is embedded in the opening tag of an element, provides further information about that element.

## REVIEW QUESTIONS

- 1. What is the meaning of Plankalkül? Who developed Plankalkül?
- 2. What was the simplest data type in Plankalkül?
- 3. How did Plankalkül implement iterations?
- 4. Speedcoding was invented to overcome two significant shortcomings of the computer hardware of the early 1950s. What were they?
- 5. Why was the technique used by Short Code called automatic programming?
- 6. In what year was IBM 704 introduced?
- 7. Where was Fortran developed? By whom?
- 8. Under what environmental constraints was Fortran developed?
- 9. How were data types specified for variables in Fortran I?
- 10. What was the most significant feature added to Fortran II to get Fortran IV?
- 11. What syntactic changes did Fortran 90 include?
- 12. Which version of Fortran was the first to support object-oriented programming?
- 13. Which version of Fortran was the first to have local scopes?
- 14. Why was Fortran list processing language (FLPL) designed and implemented as an extension to Fortran?
- 15. Where was Lisp developed? By whom?
- 16. In what ways do Scheme and metalanguage (ML) differ from each other?
- 17. What are the features of F# that make it unique?
- 18. What are the goals of the new language developed by GAMM and ACM?
- 19. In what version of ALGOL did the concept of data type appear?
- 20. What were the most important modifications made to ALGOL 58?
- 21. What change did ALGOL provide regarding input and output statements?
- 22. On what programming language was COBOL based?
- 23. In what year did the Basic design process begin?
- 24. How does COBOL allow variable names to be truly connotative?
- 25. What organization was most responsible for the early success of COBOL (in terms of extent of use)?
- 26. What were the objectives behind developing Basic?
- 27. Why is Alan Cooper known as “the father of Visual Basic”?
- 28. What facilities did PL/I provide?
- 29. What are the two fundamental characteristics shared by APL and SNOBOL?
- 30. What features of SIMULA 67 are now important parts of some object-oriented languages?
- 31. What innovation of data structuring was introduced in ALGOL 68 but is often credited to Pascal?
- 32. What was the primary deficiency of ALGOL 60?
- 33. Which language was used for teaching programming in the 1970s?
- 34. What operators in C were modeled on similar operators in ALGOL 68?
- 35. Why is C both liked and disliked?
- 36. What is a procedural language?
- 37. What are the two kinds of statements that populate a Prolog database?
- 38. What is the primary application area for which Ada was designed?
- 39. What are the concurrent program units of Ada called?
- 40. What are the different mechanisms in C that show that it was influenced by ALGOL 68?
- 41. Why did Ada 95 lose its popularity?
- 42. What is the meaning of operator overloading in C++?
- 43. What additional feature did the release 3.0 of C++ provide?
- 44. From what language does Objective-C borrow its syntax for method calls?
- 45. What is the primary application for Objective-C?
- 46. What do the Ada and COBOL languages have in common?
- 47. What are threads in Java?
- 48. What characteristic of Java is most evident in JavaScript?
- 49. How does the typing system of PHP and JavaScript differ from that of Java?
