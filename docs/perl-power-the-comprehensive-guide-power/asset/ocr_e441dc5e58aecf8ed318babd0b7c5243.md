```
$NL = "\n"
$TestString = 'It is winter and snow lies on the roof.';
print "String is '$TestString $NL";
```

Using the binding operator =~ , you can explore whether a given term matches the literal string
and the binding operator. When you use the binding operator to create regexes, it is common to
set up a form of if selection statement that Perl accommodates and that often proves easier to
use than the standard form. Consider, for example, testing whether snow matches a term in
$TestString:

```
print("Found 'snow' $NL ") if($TestString =~ m/snow/);
```

The if statement follows the call to the print() function, and you do not use a block involving
curly braces. Since the if selection statement evaluates the expression and finds the match, it
returns true, and the print() function executes. Here is the output:

```
Found 'snow'
```

In standard form, the statement appears as follows:

```
if ($TestString =~ m/snow/) {
print("Found 'snow' $NL ");
}
```

Here is the output:

```
Found 'snow'
```

# ## Identifiers

Regular expressions accommodate identifiers without problems. As shown in Listing15_01,
consider a situation in which you assign a literal string to an identifier ($Pattern) to create a
matching operation:

```
#Listing15_01
$NL = "\n"
$TestString = 'It is winter and snow lies on the roof.';
$Pattern = 'and';
print "Found literal string \\'and\\'"
if ($TestString =~ m/$Pattern/);
```

The matching function evaluates the literal string the identifier stores and returns true. The return
result is as follows:

```
Found literal string 'and'
```