> > Use the double type for floating-point numbers.

When a fractional part is required (such as in the number 0.355), we use **floating-point numbers**. The most commonly used type for floating-point numbers in C++ is called double. (If you want to know the reason, read Special Topic 2.1 on page 38.) Here is the definition of a floating-point variable:

```
    double can_volume = 0.355;
```

When a value such as 6 or 0.355 occurs in a C++ program, it is called a number literal. Table 2 shows how to write integer and floating-point literals in C++.

# ### 2.1.3 Variable Names

When you define a variable, you should pick a name that explains its purpose. For example, it is better to use a descriptive name, such as `can_volume`, than a terse name, such as `cv`.

In C++, there are a few simple rules for variable names:

+   1. Variable names must start with a letter or the underscore (`_`) character, and the remaining characters must be letters, numbers, or underscores.
+   2. You cannot use other symbols such as `$` or `%`. Spaces are not permitted inside names either. You can use an underscore instead, as in `can_volume`.
+   3. Variable names are **case-sensitive**, that is, `can_volume` and `can_Volume` are different names. For that reason, it is a good idea to use only lowercase letters in variable names.
+   4. You cannot use **reserved words** such as `double` or `return` as names; these words are reserved exclusively for their special C++ meanings. (See Appendix B.)

Table 3 shows examples of legal and illegal variable names in C++.

**Table 3 Variable Names in C++**

| Variable Name | Comment |
|---|---|
| `can_volume1` | Variable names consist of letters, numbers, and the underscore character. |
| `x` | In mathematics, you use short variable names such as `x` or `y`. This is legal in C++, but not very common, because it can make programs harder to understand (see Programming Tip 2.1 on page 38). |
| ⚠️ `can_Volume` | **Caution:** Variable names are case-sensitive. This variable name is different from `can_volume`. |
| 🚫 `6pack` | **Error:** Variable names cannot start with a number. |
| 🚫 `can volume` | **Error:** Variable names cannot contain spaces. |
| 🚫 `double` | **Error:** You cannot use a reserved word as a variable name. |
| 🚫 `1tr/fl.02` | **Error:** You cannot use symbols such as / or . |