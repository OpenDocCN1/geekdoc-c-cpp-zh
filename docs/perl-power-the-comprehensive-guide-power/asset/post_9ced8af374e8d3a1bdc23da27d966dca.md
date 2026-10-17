

function name, and then a scalar. The interpreter processes the combination without problems. Still, the readability of the code is questionable.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_82_0.png)

**Figure 4.2**
You can use different forms of syntax with functions and achieve the same results.

# Changing the Cases of Strings

As the use of the `uc()` function in the previous section indicated, Perl offers you functions that allow you to change the case of characters in strings. Some of the functions affect only the starting characters of a string. Others allow you to change all the characters in a string. This section provides a review of these functions.

# Case with First Characters

If you want to change the first character of a string to upper- or lowercase, you can do so through the `ucfirst()` and `lcfirst()` functions. Consider Listing04_02:

```perl
#Listing04_02
#Changing the cases of first letters in strings
#The first letter of the writer's name remains lowercase
$NameToChange = "herman Melville";
print "\nPrior to capitalization: " . $NameToChange;

#Assign the scalar back to itself
$NameToChange = ucfirst($NameToChange);
print "\nAfter capitalization: " . $NameToChange;

#Change the first letter back to lowercase
$NameToChange = lcfirst($NameToChange);
print "\nRestored to original: " . $NameToChange;
```

# CHAPTER 4 Print Functions

In Listing04_03, you first assign the name of the poet to a scalar, $NameToChange. You then pass the scalar as an argument to the `uc()` function, which converts the string containing the poet’s name to uppercase. Notice that, as before, to make the conversion effective, you must assign the string back to itself. The `lc()` function converts the string to lowercase. Again, you must assign the string back to itself to make the conversion effective. Figure 4.4 illustrates the output of Listing04_03.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_84_0.png)

# Obtaining the Length of a String

To obtain the length of a string, you employ the Perl `length()` function. Like the `uc()` and `print()` functions, the `length()` function requires a string for an argument. Unlike these functions, it returns a value that is not itself a string. The value that it returns is an integer that indicates the number of characters in the string. Listing04_04 illustrates some uses of the `length()` function:

```perl
#Listing04_04
#Use the length() function

#1 Basic string
#characters in the first line: 22
#characters in the second line: 40
#white spaces are counted as characters
($PreludeLines = <<WORDW);
I should learn to love
The end of life and everything we know.
WORDW

#2.Print the lines
print("\n". "$PreludeLines" . "\n");
```

64
TEAM LinG

```perl
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

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_85_0.png)

**Figure 4.5**
Use the `length()` function to obtain string lengths with white spaces.

# Hidden Characters and Strings

It often happens that when you process a string, a newline character concludes the string. Such characters are not visible and can create problems if you want to compare strings with each other. The eq operator, for instance, does not find a string containing a newline character equal to another that lacks a newline character even if all the characters other than the newline characters are the same in the two strings.

# Hidden Characters in Strings

Figure 4.6 illustrates two lines from the poetry of W. H. Auden. The first set of lines contains hidden characters. The second set contains no such characters.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_86_0.png)

**Figure 4.6**
Lines from W. H. Auden’s “Fish in the Unruffled Lakes” shows extra characters.

Comparison of the two lines illustrated in Figure 4.6 results in the wrong outcome if you are examining the lines only on the basis of whether the two sets of text you see are equal. Consider Listing04_05:

```text
#Listing04_05
#1 Set up lines with and without hidden newline characters
$CoupleALineA= "Sighs for folly said and done\n";
$CoupleALineB= "Twist our narrow days\n";
#without
$CoupleBLineA= "Sighs for folly said and done";
$CoupleBLineB= "Twist our narrow days";

#2 Print to show visual equality but different lengths
print("\nA--A: " . $CoupleALineA . "\n");
print("\nA--B: " . $CoupleALineB . "\n");
print length($CoupleALineA);
```

```perl
print("\nA-A: ". $CoupletBLineA . "\n");
print("\nA-B: ". $CoupletBLineB . "\n");
print length($CoupletBLineA);
```

```perl
#3 Compare the lines to show the interpreter
#considers them to be different
if($CoupletALineA eq $CoupletBLineA)
{
	#Does not print since equal operator returns false
	print "\nLines are the same."
}
if($CoupletALineA ne $CoupletBLineA)
{
	#Prints since the not equal operator returns true
	print "\nLines are not the same."
}
```

At comment #1 in Listing04_05, you establish two sets of strings. You attach newline characters to the first set but leave them off the second set. Then you assign the two sets of strings to scalars. In the lines associated with comment #2, you print the two couplets to show their visible resemblance, but you also employ the length() function to evaluate their lengths. Appearances indicate the lines equal each other, but from the returned values of the length() function you see that hidden characters leave them unequal. In the lines comment #3 identifies, you conduct a test using selection statements and the eq and ne operators. Figure 4.7 shows you the results. The selection statements indicate that the interpreter finds the strings unequal.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_87_0.png)

**Figure 4.7**
Unseen characters render the strings unequal.

# Eliminating Characters

Perl provides the chomp() and chop() functions to eliminate characters from the ends of strings. The chomp() function receives the greatest use since it eliminates newline characters and removes no characters other than the newline character.

# Using the chomp() Function

The chomp() function directly addresses the problem illustrated in Figure 4.7, in which the interpreter finds two strings that visibly possess the same characters to be unequal. The lack of equality results from hidden characters attached at the ends of lines. Listing04_06 illustrates the use of the chomp() function:

```perl
#Listing04_06

#1 Set up lines with and without hidden end-of-line characters
$CoupletALineA= "Sighs for folly said and done\n";
$CoupletALineB= "Twist our narrow days\n";

#Use Chomp to remove the hidden end-of-line characters
print "\nWith hidden EOL:" . chomp($CoupletALineA);
print "\nWith hidden EOL:" . chomp($CoupletALineB);

#without
$CoupletBLineA= "Sighs for folly said and done";
$CoupletBLineB= "Twist our narrow days";

print "\nWithout hidden EOL:" . chomp($CoupletBLineA);
print "\nWithout hidden EOL:" . chomp($CoupletBLineB);

#2 Print to show visual equality but different lengths
print "\nA-A: " . $CoupletALineA . "\n";
print "\nA-B: " . $CoupletALineB . "\n";
print length($CoupletALineA);

print "\nA-A: " . $CoupletBLineA . "\n";
print "\nA-B: " . $CoupletBLineB . "\n";
print length($CoupletBLineA);

#3 Compare the lines to show the interpreter
#considers them to be different
```

