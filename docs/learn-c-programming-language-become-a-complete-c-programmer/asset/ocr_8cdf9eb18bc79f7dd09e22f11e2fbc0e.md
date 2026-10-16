# Locales

> *When in Rome, do as the Romans do.*  
> —Proverb

+   - Handling Cultural Differences
+   - Class `locale`
+     Named `locales`; Comparing `strings`
+   - Class `facet`
+   
+   Accessing `facets` in a `locale`; A Simple User-defined `facet`; Uses of `locales` and `facets`
+   - Standard `facets`
+     `string` Comparison; Numeric Formatting; Money Formatting; Date and Time Formatting; Character Classification; Character Code Conversion; Messages
+   - Convenience Interfaces
+     Character Classifications; Character Conversions; String Conversions; Buffer Conversions
+   - Advice

# 39.1 Handling Cultural Differences

A `locale` is an object that represents a set of cultural preferences, such as how strings are compared, the way numbers appear as human-readable output, and the way characters are represented in external storage. The notion of a *locale* is extensible so that a programmer can add new `facets` to a `locale` representing locale-specific entities not directly supported by the standard library, such as postal codes (zip codes) and phone numbers. The primary use of `locales` in the standard library is to control the appearance of information written to an `ostream` and the format of data read by an `istream`.

This chapter describes how to use a `locale`, how a `locale` is constructed out of `facets`, and how a `locale` affects an I/O stream.

The notion of a locale is not primarily a C++ notion. Most operating systems and application environments have a notion of locale. Such a notion is – in principle – shared among all programs on a system, independently of which programming language they are written in. Thus, the C++ standard-library notion of a locale can be seen as a standard and portable way for C++ programs to access information that has very different representations on different systems. Among other things, a C++ `locale` is an interface to system information that is represented in incompatible ways on different systems.

Consider writing a program that needs to be used in several countries. Writing a program in a style that allows that is often called *internationalization* (emphasizing the use of a program in many countries) or *localization* (emphasizing the adaptation of a program to local conditions). Many of the entities that a program manipulates will conventionally be displayed differently in those countries. We can handle this by writing our I/O routines to take this into account. For example:

```
`void print_date(const Date& d) // printing the appropriate format`
```