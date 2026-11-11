# ## 8.2 Invaluable Value

Patterns added priceless value to software development in general. Of course, this also holds for concurrency in particular. The added value boils down to three points. A well-defined terminology, improved documentation, and learning from the best.

The **well-defined terminology** means that software developers can now use common and unambiguous vocabulary. Misunderstandings or verbose explanations are mainly stories of the past. Suppose a software developer asks for advice about implementing a family of similar algorithms to exchange them during runtime. In that case, the answer may be as short as use the strategy pattern. If the software developer knows the strategy pattern, he can immediately think about its consequences; if not, he can look it up in the literature.

The **documentation improves** in two aspects. First, the documentation about the software system, whether in a graphical or textual description, improves because if I read that the observer pattern is used, I know that the system has a kind of Subject/Observer structure. This means that the observer will register or unregister themselves on the subject, and the subject will send notifications to all of its observers if necessary. Secondly, I can directly jump into the source code and search for keywords such as observer, subject or notify because I have an idea about the concrete implementation.

Patterns are just about **learning from the best**. You learn from the documented experience from the best and do not repeat their mistakes. They provide proven solutions for typical problems and help to master complexity. Each pattern includes information on when you should use it, the consequences of using it, how to implement it, and its known usages.

# ## 8.3 Pattern versus Best Practices

You may wonder that I write in this part of the book also about best practices. Why? Honestly, I often had an intensive fight if a method such as immutable values or pure functions is a pattern or just best practice. Patterns are documented best practices and, therefore, quite related. I learned from these fight lessons.

+   - Both terms can not be precisely distinguished.
+   - If the practice I describe is a well-defined pattern, I put it in the pattern bucket.
+   - If the practice has a tip character and no formal defined structure, I put it in the best practices bucket.
+   - Today’s best practices may become tomorrow’s well-defined patterns.

# ## 8.4 Anti-Pattern

A pattern stands for best practices, an anti-pattern stands for a lesson learned, or to use the words from Andrew Koenig⁴: “Those that describe a bad solution to a problem which resulted in a bad

⁴https://en.wikipedia.org/wiki/Andrew_Koenig_(programmer)