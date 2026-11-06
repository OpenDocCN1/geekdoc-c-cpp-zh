# # *Section E.5 Conditional Compilation*

+   - Conditional compilation enables you to control the execution of preprocessing directives and the compilation of program code.
+   - The conditional preprocessing directives evaluate constant integer expressions. Cast expressions, `sizeof` expressions and enumeration constants cannot be evaluated in preprocessing directives.
+   - Every `#if` construct ends with `#endif`.
+   - Directives `#ifdef` and `#ifndef` are provided as shorthand for `#if defined(name)` and `#if !defined(name)`.
+   - A multiple-part conditional preprocessor construct is tested with directives `#elif` and `#else`.