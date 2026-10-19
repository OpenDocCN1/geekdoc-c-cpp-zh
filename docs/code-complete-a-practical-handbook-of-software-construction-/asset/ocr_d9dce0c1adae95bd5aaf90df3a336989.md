# # Naming Constants

> **Cross-Reference** For details on using named constants, see Section 12.7 “Named Constants.”

When naming constants, name the abstract entity the constant represents rather than the number the constant refers to. *FIVE* is a bad name for a constant (regardless of whether the value it represents is 5.0). *CYCLES_NEEDED* is a good name. *CYCLES_NEEDED* can equal 5.0 or 6.0. *FIVE = 6.0* would be ridiculous. By the same token, *BAKERS_DOZEN* is a poor constant name; *DONUTS_MAX* is a good constant name.

# ## 11.3 The Power of Naming Conventions

Some programmers resist standards and conventions—and with good reason. Some standards and conventions are rigid and ineffective—destructive to creativity and program quality. This is unfortunate since effective standards are some of the most powerful tools at your disposal. This section discusses why, when, and how you should create your own standards for naming variables.

# ### Why Have Conventions?

Conventions offer several specific benefits:

+   - They let you take more for granted. By making one global decision rather than many local ones, you can concentrate on the more important characteristics of the code.
+   - They help you transfer knowledge across projects. Similarities in names give you an easier and more confident understanding of what unfamiliar variables are supposed to do.
+   - They help you learn code more quickly on a new project. Rather than learning that Anita’s code looks like this, Julia’s like that, and Kristin’s like something else, you can work with a more consistent set of code.
+   - They reduce name proliferation. Without naming conventions, you can easily call the same thing by two different names. For example, you might call total points both *pointTotal* and *totalPoints*. This might not be confusing to you when you write the code, but it can be enormously confusing to a new programmer who reads it later.
+   - They compensate for language weaknesses. You can use conventions to emulate named constants and enumerated types. The conventions can differentiate among local, class, and global data and can incorporate type information for types that aren’t supported by the compiler.