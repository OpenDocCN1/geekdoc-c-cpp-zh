# Eliminating Characters

Perl provides the chomp() and chop() functions to eliminate characters from the ends of strings. The chomp() function receives the greatest use since it eliminates newline characters and removes no characters other than the newline character.

# Using the chomp() Function

The chomp() function directly addresses the problem illustrated in Figure 4.7, in which the interpreter finds two strings that visibly possess the same characters to be unequal. The lack of equality results from hidden characters attached at the ends of lines. Listing04_06 illustrates the use of the chomp() function:

```
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
```