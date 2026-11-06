# # Chapter 3: Reading with
Input Streams

# ### In This Chapter

+   - ✓ Reading with the extraction operators
+   - ✓ Dealing with the end of the file
+   - ✓ Reading various data types
+   - ✓ Reading data that is formatted with text

Well, isn't this nice. You have a file that you wrote to, but you need to read from it! After all, what good is a file if it's just sitting on your hard drive collecting dust?

In this chapter, we show you how you can read from a file. Reading a file is tricky because you can run into some formatting issues. For example, you may have a line of text in a file with a sequence of 50 digits. Do those 50 digits correspond to 50 one-digit numbers, or maybe 25 two-digit numbers, or some other combination? If you created the file, you probably know; but the fun part is getting your C++ application to properly read from them. The file might contain 25 two-digit numbers, in which case you make sure that the C++ code doesn't just try to read one enormous 50-digit number. In this chapter, we give you all the dirt on getting the dust off your hard drive and the file into memory. Have at it!

# ## Extracting with Operators

When you read from a file, you can use the *extraction* operator, >>. This operator is very easy to use, provided you recognize that the phrase, “Look mom, no caveats!” just doesn't apply to the extraction operator.

Suppose you have a file called `Numbers.txt` with the following text on one line:

```
`100 50 30 25`
```