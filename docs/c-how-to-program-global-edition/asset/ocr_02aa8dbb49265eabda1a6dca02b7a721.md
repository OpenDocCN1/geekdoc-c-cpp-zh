+   8.1 Introduction
+   8.2 Fundamentals of Strings and Characters
+   8.3 Character-Handling Library
+   8.3.1 Functions isdigit, isalpha, isalnum and isxdigit
+   8.3.2 Functions islower, isupper, tolower and toupper
+   8.3.3 Functions isspace, iscntrl, ispunct, isprint and isgraph
+   8.4 String-Conversion Functions
+   8.4.1 Function strtod
+   8.4.2 Function strtol
+   8.4.3 Function strtoul
+   8.5 Standard Input/Output Library Functions
+   8.5.1 Functions fgets and putchar
+   8.5.2 Function getchar
+   8.5.3 Function scanf
+   8.5.4 Function sscanf
+   8.6 String-Manipulation Functions of the String-Handling Library
+   8.6.1 Functions strcpy and strncpy
+   8.6.2 Functions strcat and strncat
+   8.7 Comparison Functions of the String-Handling Library
+   8.8 Search Functions of the String-Handling Library
+   8.8.1 Function strchr
+   8.8.2 Function strcspn
+   8.8.3 Function strpbrk
+   8.8.4 Function strrchr
+   8.8.5 Function strspn
+   8.8.6 Function strstr
+   8.8.7 Function strtok
+   8.9 Memory Functions of the String-Handling Library
+   8.9.1 Function memcpy
+   8.9.2 Function memmove
+   8.9.3 Function memcmp
+   8.9.4 Function memchr
+   8.9.5 Function memset
+   8.10 Other Functions of the String-Handling Library
+   8.10.1 Function strerror
+   8.10.2 Function strlen
+   8.11 Secure C Programming
+   Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises | Special Section: Advanced String-Manipulation Exercises | A Challenging String-Manipulation Project | Making a Difference

# 8.1 Introduction

This chapter introduces the C standard library functions that help us process strings and characters. The functions enable programs to process characters, strings, lines of text and blocks of memory. The chapter discusses the techniques used to develop editors, word processors, page-layout software, computerized typesetting systems and other kinds of text-processing software. The text manipulations performed by formatted input/output functions like printf and scanf can be implemented using the functions discussed in this chapter.

# C11 Annex K Functions

As we discuss in Section 8.11, C11's optional Annex K describes more secure versions of many functions that we present in this chapter. As with printf_s and scanf_s for printf and scanf, the more secure Annex K versions should be used, if available for your compiler.

# 8.2 Fundamentals of Strings and Characters

Characters are the fundamental building blocks of source programs. Every program is composed of a sequence of characters that—when grouped together meaningfully—is in-