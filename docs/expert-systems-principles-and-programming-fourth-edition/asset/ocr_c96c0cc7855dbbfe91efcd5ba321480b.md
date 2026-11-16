shown in this and the following chapters should work on any computer on which CLIPS has been installed. It is recommended that CLIPS users have some knowledge of the operating system of the computer on which CLIPS is being used. For example, the method of specifying files tends to vary from one operating system to another. When commands may vary depending on the machine or the operating system, this will be noted.

# 7.3 NOTATION

This chapter and those following will use the same notation for describing the syntax of various commands and constructs that are introduced. This notation consists of three different types of text to be entered.

The first type of notation is for symbols and characters that are to be entered exactly as shown; this includes anything that is not enclosed by the character pairs <>, [ ], or { }. For example, consider the following syntax description:

```
(example)
```

This syntax description means that (example) should be entered as shown. To be exact, the character “(” should be entered first, followed by the character “e,” then “x,” “a,” “m,” “p,” “l,” “e,” and finally the character “).” Square brackets, [ ], indicate that the contents of the brackets are optional. For example, the syntax description:

```
(example [1])
```

indicates that the 1 found within the brackets is optional. So the following entry would be consistent with the above syntax:

```
(example)
```

as would this entry:

```
(example 1)
```

The less than and greater than characters together, <>, indicate that a replacement is to be made with a value of the type specified by the contents found within the <>. For example, the following within a syntax description:

```
<integer>
```

indicates that a substitution should be made with an actual integer value. Following the previous examples, the syntax description:

```
(example <integer>)
```