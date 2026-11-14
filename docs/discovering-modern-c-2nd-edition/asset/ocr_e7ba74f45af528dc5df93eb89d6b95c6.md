# Chapter 6
Object-Oriented Programming

> “We inherit nothing truly, but what our actions make us worthy of.”
> —George Chapman

C++ is a multi-paradigm language, and the paradigm that it is most strongly associated with is Object-Oriented Programming (OOP). As a result, we find all these beautiful dog-cat-mouse examples in books and tutorials. Experience shows, however, that most real software packages do not contain such deep class hierarchies as the literature makes us believe. It is furthermore our experience that generic programming is the superior paradigm in scientific and engineering programming because:

+   - It is more flexible: polymorphism is not limited to sub-classes; and
+   - It provides better performance: no overhead in indirect function calls.

We will explain this in more detail within this chapter.

On the other hand, inheritance can help us to increase productivity when multiple classes share data and functionality. Accessing inherited data is free of overhead, and even calling inherited methods has no extra cost when they are not virtual.

The great benefit of object-oriented programming is the run-time polymorphism: which implementation of a method is called can be decided at run time. We can even select class types during execution. The before-mentioned overhead of virtual functions is only an issue when very fine-grained methods (like element access) are virtual. Conversely, when we