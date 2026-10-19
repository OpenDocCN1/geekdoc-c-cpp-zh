```
Java Example of Using Complicated Logic to Classify a Character
if ( ( ( 'a' <= inputChar ) && ( inputChar <= 'z' ) ) ||
    ( ( 'A' <= inputChar ) && ( inputChar <= 'Z' ) ) ) {
    charType = CharacterType.Letter;
}
else if ( ( inputChar == ' ' ) || ( inputChar == ',' ) ||
    ( inputChar == '.' ) || ( inputChar == '!' ) || ( inputChar == '(' ) ||
    ( inputChar == ')' ) || ( inputChar == ':' ) || ( inputChar == ';' ) ||
    ( inputChar == '?' ) || ( inputChar == '-' ) ) {
    charType = CharacterType.Punctuation;
}
else if ( ( '0' <= inputChar ) && ( inputChar <= '9' ) ) {
    charType = CharacterType.Digit;
}
```

If you used a lookup table instead, you’d store the type of each character in an array that’s accessed by character code. The complicated code fragment just shown would be replaced by this:

```
Java Example of Using a Lookup Table to Classify a Character
charType = charTypeTable[ inputChar ];
```

This fragment assumes that the charTypeTable array has been set up earlier. You put your program’s knowledge into its data rather than into its logic—in the table instead of in the if tests.

# Two Issues in Using Table-Driven Methods

![](bbox=[0.1, 0.58, 0.2, 0.65])

When you use table-driven methods, you have to address two issues. First you have to address the question of how to look up entries in the table. You can use some data to access a table directly. If you need to classify data by month, for example, keying into a month table is straightforward. You can use an array with indexes 1 through 12.

Other data is too awkward to be used to look up a table entry directly. If you need to classify data by Social Security Number, for example, you can’t use the Social Security Number to key into the table directly unless you can afford to store 999-99-9999 entries in your table. You’re forced to use a more complicated approach. Here’s a list of ways to look up an entry in a table:

+   - Direct access
+   - Indexed access
+   - Stair-step access

Each of these kinds of accesses is described in more detail in subsections later in this chapter.