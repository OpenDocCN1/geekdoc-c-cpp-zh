# CHAPTER 15 } Regular Expressions

```
Test for words.
Match 1: mast
Match 1: mart
Match 1: mort
Match 1: moot
Match 1: must
Match 1: mist
```

# The Comma (Multiplier) as a Range Setting

You can use the comma with the curly braces to multiply a given character. In Example 7 of Listing15_05, the words in the list starting with de and ending with te are all candidates. Between these characters, you allow an acceptable number of occurrences that match the pattern.

```
@WordList = qw(deracinate designate demote denigrate demonstrate);
print "\nTest for words.\n";
foreach $Word (@WordList) {
    print "\nMatch 2: $Word" if ($Word =~ m/de.{2,6}te/);
}
```

In the set given, the expression finds only demonstrate because seven characters lie between the selected groups. This is the only word long enough to exceed the range. Here is the output of this part of Example 7 in Listing15_05:

```
Test for words.
Match 2: deracinate
Match 2: designate
Match 2: demote
Match 2: denigrate
```

If you drop the second number and the comma, you abolish the range, so the expression allows for only words that have two characters between the named characters. This reduces the field considerably. The only word that meets this narrow stipulation is demote. Here is the output of this part of Example 7 in Listing15_05:

```
Test for words.
Match 3: demote
```

# The Asterisk (*)

When you employ an asterisk you achieve a result similar to using braces or periods. Asterisks indicate that you are allowing any number of characters. In the following example, a is followed