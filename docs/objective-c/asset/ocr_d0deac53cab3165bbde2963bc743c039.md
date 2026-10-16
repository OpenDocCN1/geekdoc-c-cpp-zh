# 4 Understanding Objective-C Memory Management

One of the biggest challenges you may face as a new Objective-C developer when coming to the platform from other languages, such as Java, Ruby, and Python, is that Objective-C requires that you think about memory management. Many other modern languages have built-in memory management systems (garbage collection, for example) which enable the programmer to ignore most memory management concerns. Objective-C has a garbage collected runtime version, but it is relatively new to the language and unavailable when working on some of the platforms that Objective-C runs on, such as iPhone and iPad. As a result, while it would be nice to say that a new Objective-C developer has no need to be concerned about memory management, doing so would be a disservice to you as a new student of Objective-C. It is entirely likely that even if you are not writing Objective-C code for platforms other than MacOS X, you will still run into MacOS X code, which does not have garbage collection and requires you to manage your memory manually.

Fortunately, however, if you become familiar with the Objective-C memory management rules, even managing your memory by hand can be a reasonably simple affair. By the time you finish this chapter, you should have all of the knowledge of all of the tools that you will require to work with both memory managed code as well as non-memory managed code.

# Using Reference Counting

Before I begin reviewing the actual tools that you will use to manage your memory in Objective-C, I first want to introduce you to the mechanism that Objective-C uses under the hood to make manual memory management almost as easy as using a garbage-collected environment.

Every object that inherits from NSObject inherits certain memory management behaviors. Internal to these objects there exists a counter called the retain count. Using certain calls, this counter can

# In This Chapter

+   - Introducing memory management
+   - Using reference counting
+   - Building objects that manage memory
+   - Using garbage collection
+   - Converting existing code to garbage collection
+   - Knowing what memory management model to use