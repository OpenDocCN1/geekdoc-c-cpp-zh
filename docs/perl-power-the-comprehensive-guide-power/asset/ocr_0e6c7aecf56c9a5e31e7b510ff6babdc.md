function name, and then a scalar. The interpreter processes the combination without problems. Still, the readability of the code is questionable.

![](bbox=[0.369, 0.171, 0.848, 0.395])

**Figure 4.2**
You can use different forms of syntax with functions and achieve the same results.

# Changing the Cases of Strings

As the use of the `uc()` function in the previous section indicated, Perl offers you functions that allow you to change the case of characters in strings. Some of the functions affect only the starting characters of a string. Others allow you to change all the characters in a string. This section provides a review of these functions.

# Case with First Characters

If you want to change the first character of a string to upper- or lowercase, you can do so through the `ucfirst()` and `lcfirst()` functions. Consider Listing04_02:

```
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
```