# CHAPTER 15 } Regular Expressions

```
```perl
$ResultString = "Tell me about the world as a world in the world";
$_ = $ResultString;
$_ = s/world/place/g;
print "$NL Revised: $_";
```
```

As the output indicates, the substitution of place for world occurs even though you see no binding operator. The set of statements depends on the reader’s understanding that the system variable works along the lines of the argument array and return values of functions. It receives a value. The selection statement implicitly receives its target from the system variable. Because the substitution statement returns the transformed string, you are able to retrieve this value from the system variable to form the interpolated string for the print() function. Here is the output from the print() function:

```
```text
Revised: Tell me about the place as a place in the place.
```
```

Because the system variable allows you to capture the result of a previous statement, you can alter a foreach operation using the list function so that it appears in an abbreviated form:

```
```perl
foreach ( "canada", "mexico", "peru", "brazil") {
    print "Not " . ucfirst($_) . " $NL";
    if($_ =~ m/brazil/) {
        print "But " . ucfirst($_) . " $NL";
    }
}
```
```

The result of Example 2 in Listing15_3 shows you that the repetition statement traverses the list using the system variable.

# Translation

Translation offers you a way to effect operations that in many ways resemble those you accomplish using substitutions. When you translate a string, you can operate on existing characters. When you substitute, you can completely alter the length and content of a string. Listing15_04 provides a few examples that combine substitution and translation. In a few instances, such as reversing strings, you enjoy great advantages by using the translation function.

# Reversing Strings

The translation function allows you to reorder the characters in strings according to a range and an order you provide in the translation argument. Example lin Listing15_04 reverses a string of numbers.