# CHAPTER 21

# Reflection

# IN THIS CHAPTER

+   - Typing Revisited, Static and Otherwise 1048
+   - Reflection 1054
+   - Lightweight Code Generation 1082
+   - Expression Trees 1091

So far, we've been looking at statically typed code for the most part. In the world of static typing, it's the compiler's task to resolve information about types at the point the program is compiled. This provides various benefits related to program checks for various forms of correctness, improved tooling support thanks to IntelliSense, increased runtime performance because operations are known unambiguously, and much more.

However, such static type information is not always available. And although the benefits mentioned should be enough to convince people to get static typing wherever possible, the harsh reality is there are many dynamically typed pieces of code and data out there. In fact, we've seen an increasing trend moving away from static typing for various types of systems, such as web services (without a WSDL definition, and using REST) and data formats like XML (without XSD schema) or JSON.

In this chapter, we look at the facilities provided by the common language runtime and the .NET Framework to interoperate with objects lacking static type information. This stretches reflection and on-the-fly code generation. In the next chapter, we look at the dynamic keyword introduced in C# 4.0, which in part builds on the services explained in this chapter.