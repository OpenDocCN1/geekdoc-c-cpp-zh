# 25

# Specialization

> *It ain’t what you don’t know that gets you into trouble. It’s what you know for sure that just ain’t so.*
> — Mark Twain

+   - Introduction
+   - Template Parameters and Arguments
+   Types as Arguments; Values as Arguments; Operations as Arguments; Templates as Arguments; Default Template Arguments
+   - Specialization
+   Interface Specialization; The Primary Template; Order of Specialization; Function Template Specialization
+   - Advice

# 25.1 Introduction

Over the last two decades, templates have developed from a relatively simple idea to the backbone of most advanced C++ programming. In particular, templates are key to techniques for

+   - improving type safety (e.g., by eliminating the use of casts; §12.5);
+   - raising the general level of abstraction of programs (e.g., by using standard containers and algorithms; §4.4, §4.5, §7.4.3, Chapter 31, Chapter 32); and
+   - providing more flexible, type-safe, and efficient parameterization of types and algorithms (§25.2.3).

These techniques all critically rely on the ability of template code to use template arguments without overhead and in a type-safe manner. Most techniques also rely on the type deduction mechanisms offered by templates (sometimes called *compile-time polymorphism*; §27.2). These techniques are the backbone of C++ use in performance-critical areas, such as high-performance numerical computing and embedded systems programming. For mature examples, see the standard library (Part IV).

This chapter and the following two present simple examples of the advanced and/or specialized language features supporting techniques aimed at uncompromised flexibility and performance. Many of these techniques are primarily developed for and used by library implementers. Like most programmers, I prefer to forget about the more advanced techniques most of the time. Where I can, I keep my code simple and rely on libraries so that I can benefit from the use of advanced features in the hands of experts in a given application domain.

Templates are introduced in §3.4. This chapter is part of a sequence presenting templates and their uses:

+   - Chapter 23 gives a more detailed introduction to templates.
+   - Chapter 24 discusses generic programming, the most common use of templates.
+   - Chapter 25 (this chapter) shows how to specialize a template with a set of arguments.