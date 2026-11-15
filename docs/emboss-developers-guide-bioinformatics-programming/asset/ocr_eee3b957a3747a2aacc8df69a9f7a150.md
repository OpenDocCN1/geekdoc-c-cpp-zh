ajpat.h/c. Defines the sequence pattern list object (AjPPatlistSeq) and general pattern list object (AjPPatlistRegex) and functions for handling lists of regular expression patterns. They contain static data structures and functions for handling sequence patterns at a low level.

You are unlikely to need the static data structures and functions unless you plan to implement code to extend the functionality of the libraries themselves.

In addition to the above library files, EMBOSS includes a library of functions to support regular expressions whose syntax and semantics are as close as possible to those of the Perl 5 language. The library files are:

```
pcre_config.h
pcre_internal.h
pcre.h
pcre.c
pcreposix.h
pcreposix.c
pcre_printint.c
pcre_chartables.c
pcre_get.c
pcre_study.c
```

They are not described here and you should see the online library documentation for further information.

# 6.6.3 ACD datatypes

There are two datatypes for handling pattern input:

+   - regexp: A regular expression pattern
+   - pattern: A sequence pattern

# 6.6.4 ACD data definition

Typical ACD definitions are shown below.

# 6.6.4.1 regexp

Regular expression input:

```
regexp: patterns
[
    information: "Regular expression patterns"
    upper: "Y"
    minlength: "3"
    minlength: "10"
]
```