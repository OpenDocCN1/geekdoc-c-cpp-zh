# ## CHAPTER 12

# # Native Methods

# ### In this chapter

+   - 12.1 Calling a C Function from a Java Program, page 810
+   - 12.2 Numeric Parameters and Return Values, page 817
+   - 12.3 String Parameters, page 819
+   - 12.4 Accessing Fields, page 825
+   - 12.5 Encoding Signatures, page 831
+   - 12.6 Calling Java Methods, page 832
+   - 12.7 Accessing Array Elements, page 840
+   - 12.8 Handling Errors, page 844
+   - 12.9 Using the Invocation API, page 849
+   - 12.10 A Complete Example: Accessing the Windows Registry, page 855

While a “100% Pure Java” solution is nice in principle, there are situations in which you will want to write (or use) code in another language. Such code is usually called *native* code.

Particularly in the early days of Java, many people assumed that it would be a good idea to use C or C++ to speed up critical parts of a Java application. However, in practice, this was rarely useful. A presentation at the 1996 JavaOne conference showed this clearly. The developers of the cryptography library at Sun Microsystems reported that a pure Java platform implementation of their cryptographic functions was more than adequate. It was true that the code was not as fast as a C implementation would have been, but it turned