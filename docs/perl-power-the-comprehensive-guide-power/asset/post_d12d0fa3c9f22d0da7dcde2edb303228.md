

## Identifiers

Regular expressions accommodate identifiers without problems. As shown in Listing15_01, consider a situation in which you assign a literal string to an identifier ($Pattern) to create a matching operation:

```
#Listing15_01
$NL = "\n"
$TestString = 'It is winter and snow lies on the roof.';
$Pattern = 'and';
print "Found literal string \\'and\\'"
if ($TestString =~ m/$Pattern/);
```

The matching function evaluates the literal string the identifier stores and returns true. The return result is as follows:

```
Found literal string 'and'
```

# CHAPTER 15 Regular Expressions

To set up a negative test, your expression takes the following form. Note the change in the binding operator:

```
if($TestString !~ m/"nowhere"/){
    print("Did prove false. $NL");
}else{
    print("Did not prove false. $NL")
}
```

The expression test determines whether nowhere is part of the tested string. The match returns nowhere Did prove false. since the expression confirms the absence of nowhere.

You can insert a string into the regex without using quotation marks. You can also combine strings with an identifier through concatenation operations. Consider a situation in which you combine the identifier $Pattern (which is defined with snow) and the literal term snow. The concatenation is implicit. A space separates the two words:

```
$Pattern = "and";

if($TestString =~m/$Pattern snow /){
    print("$NL\'$Pattern snow\' found. $NL");
}
```

The output is as follows:

```
'and snow' found.
```

The line prints because the function reads all the arguments presented to it as one continuous string, regardless of whether it is a literal or defined in an identifier.

In the following lines, you create a string that generates a false evaluation. The operation involves the use of an identifier and a literal string.

```
if($TestString =~ m/$Pattern snowz/){
    print "Found variable and literal\n";
}else{
    print "Did not find variable and literal\n";
}
```

In this case, since you have corrupted the matching string by adding a z to snow, the result match does not occur, so you see the statement in the else block.

# Match Variations

You can use a number of variations in the forms of matching you employ. The slashes are the most common delimiters, but you can change the delimiters in many ways. Consider, for example, a few basic alternatives involving matches:

```
if ($TestString =~ m!roof!){
    print("Match delimited with !! $NL");
}
if ($TestString =~ m{roof}){
    print("Match delimited with {} $NL");
}
```

In these two expressions, you substitute exclamation marks and curly braces for slashes. The output is as follows:

```
Match delimited with !!
Match delimited with {}
```

When you evaluate expressions that contain special characters, you must identify the special characters using escape sequences:

```
$EscapeTerms = "\\\$";
if ($EscapeTerms =~ m"\@"){
    print "Match with escape \@ $NL";
}
```

# Exactness

When you create a pattern, you can match almost any series of letters. In other words, the letters can be separated by spaces, other letters, or words, but the match requires (in most cases) that you match the sequence.

```
if ($TestString =~ m/ on the r/){
    print "An exact pattern works. $NL";
}
```

If you include spaces to indicate that a given word lacks completion, the match remains inexact. Consider the following matches:

```
if($TestString =~ m/ on the r /){
    print "Found on the r (space after r)$NL ";
}elseif($TestString =~ m/ on the r/){
    print " Found on the r (no space after r)$NL";
}
```

The selection produces the following result:

Found on the r (no space after r)

The first expression allows a space to occur after the r. The original expression contains no such space. The `elseif` expression evaluates true because it allows no extra space.

Along the same lines, as long as you do not imply that any spaces exist, you can match part of a word. Consider a match with a literal expression:

```
if ("Snow fell every day in February" =~ m/bru/) {
print "Found part of \'February\'.$NL" ;
}
```

You see the following result:

Found part of 'February'.

# ## Matching with Arrays or Lists

You can use the matching function in any number of ways with lists or arrays. Consider this use of the list function combined with the `foreach` selection statement:

```
foreach $Word ("howie", "howa", "howda", "howdy")
{
    if(m/howdy/) {
        print("$NL $Word IS the right word.$NL ");
    }else{
        print("$NL $Word is not right.");
    }
}
```

The `foreach` statement traverses the list, retrieving each term to `$Word`. The selection statement then evaluates each term against howdy.

howie is not right.
howa is not right.
howda is not right.
howdy IS the right word.

# Substituting

The substitution function allows you to replace a given expression with another expression. The most elementary approach to using the substitution function involves substituting one word for another. The basic substitution function replaces the first occurrence of a term you identify. As the example in Listing15_02 shows, you name the expression you want to replace in the first part of the expression. You name the replacement term in the second. Here is the example:

```
#Listing15_02
$TestStringA = "Say hello to the world.";
$ResultString = $TestStringA;
$ResultString =~ s/hello/your greetings/;
print("Result: $ResultString $NL");
```

The output appears as follows:

```
Result: Say your greetings to the world.
```

You can use the substitution statement as you traverse a string with a repetition control statement. As Example 2 in Listing15_02 shows, you can employ a repetition statement to traverse a string and sequentially alter words in the string.

```
$ResultString = "Tell me about the world as a world in the world";
$Count = 1;
do{
        print("$ResultString $NL");
        $ResultString =~ s/world/planet/;
        $Count++;
}while($Count < 5);
```

The output of Example 2 shows you how the substitution function alters a new term with each repetition of the block:

```
Tell me about the world as a world in the world
Tell me about the planet as a world in the world
Tell me about the planet as a planet in the world
Tell me about the planet as a planet in the planet
```

# Global Changes

The g (global) argument provides an alternative to using a repetition control structure. It detects all instances of the terms you have designated for substitution and changes them. Example 3 in Listing15_02 explores both how to use global substitution and how to obtain the number of substitutions the function performs:

```
$ResultString = "Tell me about the world as a world in the world";
$NumOfMatches = $ResultString =~ s/world/planet/g; #use g for global
print("$NL Word occurred $NumOfMatches times");
print("$NL $ResultString");
```

As Example 3 shows, to obtain the number of substitutions the substitution function performs, you use the assignment operator (=) along with the binding operator (=~). You can see from this operation that the entire expression returns the number of substitutions.

# ## Exactness

Successful substitution depends on providing the right criteria for substitutions. As with matching operations, substitution operations require that you be conscious of how you use white spaces.

```
$ResultString = "Tell me about the world as a world in the world";
$ResultString =~ s/w/W/g;
print("$NL Revised: $ResultString $NL");
$ResultString =~ s/a / A /g;
print("$NL Revised: $ResultString $NL");
$ResultString =~ (s/a/A/g);
print("$NL Revised: $ResultString $NL");
```

The results of the operation are as follows:

```
Revised: Tell me about the World as a World in the World
Revised: Tell me about the World as A World in the World
Revised: Tell me About the World As A World in the World
```

The substitution changes the first line because no spaces appear before or after the w argument that you insert into the substitution function. You succeed in making only one change in the second line because in the substitution function you insert white spaces before and after the w. Only one article occurs in the sentence, so the expression changes only one letter. With the third line, you see that the expression capitalizes all the As. In this instance, you have, as before, not included white space before or after the letter you want to alter.

# ## Fundamental Ranges

You can select items for substitution using the range operator. The range operator consists of a set of open and close square brackets ([ ]). Inside the brackets, you can designate two or more characters you want to change. To separate the items, you employ commas. Example 5 of Listing15_02 examines making changes to a range of letters:

