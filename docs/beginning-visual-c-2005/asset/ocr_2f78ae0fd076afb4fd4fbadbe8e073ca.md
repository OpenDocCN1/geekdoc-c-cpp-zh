Note that the two forms of #include directive in the previous code fragment cause the compiler to search for the file in different ways. When you specify the file to be included between angled brackets, you are indicating to the compiler that it should search for the file along the path specified by the /I compiler option, and failing that along the path specified by the INCLUDE environment variable. These paths locate the C+ library files, which is why this form is reserved for library headers. The INCLUDE environment variable points to the folder holding the library header and the /I option allows an additional directory containing library headers to be specified. When the file name is between double quotes, the compiler will search the folder that contains the file in which the #include directive appears. If the file is not found, it will search in any directories that #include the current file. If that fails to find the file, it will search the library directories.

# C++/CLI Programming

C++/CLI provides a number of extensions and additional capabilities to what I have discussed in this chapter up to now. I'll first summarize these additional capabilities before going into details. The additional C++/CLI capabilities are:

+   - All of the ISO/ANSI fundamental data types can be used as I have described in a C++/CLI program, but they have some extra properties in certain contexts that I'll come to.
+   - C++/CLI provides its own mechanism for keyboard input and output to the command line in a console program.
+   - C++/CLI introduces the safe_cast operator that ensures that a cast operation results in verifiable code being generated.
+   - C++/CLI provides an alternative enumeration capability that is class-based and offers more flexibility than the ISO/ANSI C++ enum declaration you have seen.

You'll learn more about CLR reference class types beginning in Chapter 4, but because I have introduced global variables for native C++, I'll mention now that variables of CLR reference class types cannot be global variables.

I want to begin by looking at fundamental data types in C++/CLI.

# C++/CLI Specific: Fundamental Data Types

You can and should use the ISO/ANSI C++ fundamental data type names in your C++/CLI programs, and with arithmetic operations they work exactly as you have seen in native C++. In addition C++/CLI defines two additional integer types:

| Type | Bytes | Range of Values |
|---|---|---|
| long long | 8 | From 9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| unsigned long long | 8 | From 0 to 18,446,744,073,709,551,615 |