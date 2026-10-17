```
#3.Obtain the length and store the value in a scalar
$CharLength = length($PreludeLines);
#Then show the results
print "\nThe number of characters in the lines,".
      "\nincluding blank spaces ".
      "(from Wordsworth's \"Prelude\")is $CharLength.";

#4.You can also just print the return value
print "\nAgain, the length: ". length($PreludeLines);
```

The lines accompanying comment #1 in Listing04_04 create a block consisting of two lines from William Wordsworth’s “The Prelude.” Preceding the creation of the block, the comments show counts of the characters, including the blank spaces, that each line contains. You store the lines in a scalar, $PreludeLines. The code affiliated with comment #2 prints these lines.

In the lines trailing comment #3, you call the length() function and provide $PreludeLines to it as its argument. The function obtains the number of characters in the lines, including white spaces, and returns this value to the scalar $CharLength. Having obtained the character length of the lines, you then print a concatenated string that interpolates the value stored in $CharLength.

At comment #4, you call the print() function to print the return value of length(). Figure 4.5 shows you the output of Listing04_04.

![](bbox=[0.148, 0.57, 0.626, 0.743])

**Figure 4.5**  
Use the `length()` function to obtain string lengths with white spaces.

# Hidden Characters and Strings

It often happens that when you process a string, a newline character concludes the string. Such characters are not visible and can create problems if you want to compare strings with each other. The eq operator, for instance, does not find a string containing a newline character equal to