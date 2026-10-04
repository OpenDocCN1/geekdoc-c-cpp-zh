# 7.3. INFORMATION FLOW CONTROL

used by the virtual machine to trap problems like array-out-of-bounds, null pointers and other common problems that are implicitly checked during bytecode interpretation. These exceptions might be thrown by many bytecode instructions requiring their declaration or in try/catch blocks seemed burdensome for the designers of the Java language. But Jif requires exactly that! Slicing-based information flow can catch the exceptions from where they are thrown to a matching catch and raises a security policy violation only if such a flow transmits information to public channels. Therefore the programmer is not overwhelmed by dealing with usual exceptions.

As an example, consider the password example in Figure 4.3 on page 93, from [ML00]. Even this trivial code requires two catch blocks, for NullPointer and IndexOutOfBounds. Both apply the dreaded crashed-all-pointer-anti-pattern, that empirical evidence shows make bug-detection a lot harder. It is in total contradiction to Dijkstra's principle of the weakest precondition and may produce hard-track inherited errors.

**Type discrimination on parameters** In casts or instanceof, Jif allows no classes that are parametrized with a security label. Like Java's generics, this is erased during compilation. This overly restrictive parameterized classes are also for code reuse [ML00, AS05]. Parameterized expressions could be permitted if the parameters statically known to be matched, but this is currently not supported.

Libraries Existing libraries are not annotated with security labels and cannot be flow-checked with Jif. While Jif wrapper classes to the most important library classes like collections, many other libraries are not supported if the source or bytecode is provided. Since Java's popularity is based to a big extent on the availability of a large standard libraries and numerous custom libraries, these restrictions impede the proliferation of security typed languages.

Regarding the limitations listed above, it becomes evident why languagebased information flow control did not gain real traction in more than ten years of its existence. Zdancevic states that "despite this body of literature and considerable, ongoing attention from the research community, information flow enforcement mechanisms have not been widely seen (or even narrowly!)" [Zda04]. Only recently some programs have been written in the Jif language, however, in the academic field [MCN+]. We argue that for practical use, a realistic language must be analyzable without major restrictions.

# 7.3.2 Slicing-Based Information Flow Control

The remainder of this section will concentrate on our new form of information flow control based on program slicing as presented in chapter 4. We will compare