# 1. PROBLEM STATEMENT

Build a concordance of a text file. Write the concordance, along with a count of the unique words in the text file, to an output file.

# 2. INPUT/OUTPUT DESCRIPTION

The following diagram shows that the input to the program is a text file, and that the output is a concordance of the text file along with the count of unique words. We will use the list class to define a list, where each element in the list is of type string.

![](bbox=[0.22, 0.27, 0.65, 0.38])

# 3. HAND EXAMPLE

Suppose our text file contained only the following text:

A concordance of a text file is an alphabetical list of the unique words in the text file.

Our program would generate the following output file:

```
a
are
13 distinct words in the text file;
an
alphabetical
concordance
file
in
is
list
of
text
the
unique
words
```

# 4. ALGORITHM DEVELOPMENT

We first develop the decomposition outline to break the solution into a series of sequential steps:

Decomposition Outline

+   1. Open input and output files.

+   2. Read a word from the input file.