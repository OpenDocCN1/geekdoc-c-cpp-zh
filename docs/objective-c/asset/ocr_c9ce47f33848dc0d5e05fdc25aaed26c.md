# Objective-C Design Patterns

One of the joys of developing with Objective-C and the Foundation framework is the fact that its designers have fully embraced the most modern of software development methodologies when thinking about engineering the API and language. Indeed, some experts argue that these methodologies even originated with Objective-C.

Among the methodologies that are well represented in Objective-C and Foundation is the concept of design patterns. In fact, evidence shows that the first implementation of many of the common design patterns that we use in programming today actually originated in the Objective-C community. Though they may not necessarily be called by their modern names, “Chain of Responsibility”, “Observer”, and so on, there can be no mistaking that the Objective-C versions of these common (today) design patterns are well represented in the Objective-C language.

In this chapter, I show you how to implement some of the more common design patterns in Objective-C. Objective-C, Foundation, and Cocoa leverage design patterns heavily within their respective APIs; therefore, you will encounter design patterns in Objective-C regularly. It can be useful to understand how these design patterns are implemented, specifically in Objective-C, because the implementation in a dynamic compiled language such as Objective-C can sometimes be slightly different than its implementation in a more strictly typed language, such as C++ or Java.

# Recognizing Patterns in Solutions

Have you ever noticed that over time, the same kinds of problems tend to appear in your application development over and over again in different projects? You might be working away, and find yourself faced with a particular programming circumstance that closely, but not exactly, matches a scenario that you just previously dealt with elsewhere. Perhaps the problem was close to another problem but not close enough that you could exactly reuse the

# In This Chapter

+   - Understanding design pattern usage in Objective-C
+   - Learning how to make a singleton in Objective-C
+   - Delegating responsibility using delegates
+   - Observing changes using notifications