correct approach first. I will also be brief here, as the main purpose of my enumeration is to help you recognize pitfalls and know when you might be on the wrong track.

There is another acronym here. STUPID describes cases where you should pause to perhaps rethink your design.[^1]

+   - **Singleton**  
+     A class with only one instance, often referred to as a *disguised global variable*. Singletons are controversially discussed and their use is often referred to as an *antipattern*.
+   
+   - **Tight coupling**  
+     The tight coupling of components is definitely bad and breaks several SOLID principles.
+   
+   - **Untestability**  
+     What you cannot test, you cannot change, and you cannot be sure if you are done. You can only refactor if you can test. The more automated the tests, the easier it is to change code.
+   
+   - **Premature optimization**  
+     Do not get bogged down with unnecessary details. Only deal with improvements when it pays off. Or even more extreme, if you are wondering whether to optimize, follow these rules: One, don't do it. Two (only for experts), don't do it yet. This is especially true for performance optimizations. In architectural matters, you will find that just writing proper tests leads to a better architecture, and the question of whether this architectural decision was the right one no longer arises.
+   
+   - **Indescriptive naming**  
+     What are `field1` to `field99`? Good names are more important than comments.
+   
+   - **Duplication**  
+     Duplicated code needs to be maintained twice and will eventually contradict itself. If you like acronyms, then stay DRY—that is, *don't repeat yourself*. When duplication threatens to arise, refactor.

As always, there are sometimes reasons for exceptions. Not every global variable and not every singleton is bad. GUIs are inherently hard to test, and some duplication simplifies the design. But exceptions should not be an excuse and should not become the rule.

[^1]: “From STUPID to SOLID Code!”, William Durand, 2013-08-30, https://williamdurand.fr/2013/07/30/from-stupid-to-solid-code/, [2024-08-12]