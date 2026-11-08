# # Move Semantics

This chapter complements and completes several key topics discussed in the middle parts of the book. In Chapters 12 and 13, for instance, you gained insight from the mechanics behind the copying of objects, that is, copy constructors and assignment operators. And from Chapter 8 you know to prefer pass-by-reference over pass-by-value to avoid undue copying of parameters. For a long time, that was basically all you needed to know. C++ offered facilities to copy objects, and if you wanted to avoid costly copies, then you simply used either references or pointers. Starting with C++11, however, there is a powerful new alternative. You can no longer only copy objects; you can now also move them.

In this chapter, we'll show you how move semantics allows you to efficiently transfer resources from one object into another, without deep copying. We also wrap up our treatment of the special class members—which you already know, the default constructor, destructor, copy constructor, and copy assignment constructor.

In this chapter, you’ll learn

+   - What the difference is between lvalues and rvalues
+   - That there's another kind of reference: rvalue references
+   - What it means to move an object
+   - How to provide so-called move semantics for objects of your own types
+   - When objects are moved implicitly and how to explicitly move them
+   - How move semantics leads to code that is both elegant and efficient
+   - What impact move semantics has on various best practices regarding defining your own functions and types
+   - The “rule of five” and “rule of zero” guidelines

# ## lvalues and Rvalues

Every single expression is either an lvalue or an rvalue (sometimes written l-value and r-value and pronounced like that). An lvalue evaluates to some persistent value with an address in memory in which you can store something or an ongoing basis; an rvalue evaluates to a result that is stored only transiently. Historically, lvalues and rvalues are so called because an lvalue expression typically appears on the left of an