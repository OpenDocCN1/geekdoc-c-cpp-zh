# CHAPTER 10 Control Structures

```
$Title = "\nMan";
$Author = "\nAmos Bronson Alcott 1799-1888";
$Source=
"\nPerry Miller, ed. The American Transcendentalists".
"\n(Baltimore: Johns Hopkins U. Press, 1957), p. 257.";
#2 Split the array using the punctuation marks
@ABAlcott = split(/[:|:|:/, $ABAlcottMan);
#3 Print the introductory lines
#Increment through the lines of the poem
#Print the source
$Itr = 0;
print "\n" . join("", $Author, $Title, "\n\n",
$ABAlcott[$Itr], $ABAlcott[++($Itr)],
$ABAlcott[++($Itr)], $ABAlcott[++($Itr)],
$ABAlcott[++($Itr)], $ABAlcott[++($Itr)],
$ABAlcott[++($Itr)], $ABAlcott[++($Itr)],
"\n", $Source);
```

At comment #1 you use a text block to create a scalar that stores the text of a poem by Amos
Alcott. You also create scalars that identify the author, title, and source text of the poem. In the
lines that comment #2 identifies, you use the split() function to separate the lines of the
poem into elements of an array (@ABAlcott). The split() function contains a regular
expression that consists of three punctuation marks, a semicolon, a comma, and a colon
(/[:|:|:/). The two slashes serve to bound the regular expression. The pipes (|) separate the
items and indicate that any one of them can be used as a separator for the text the split()
function processes.

In the lines associated with comment #3, you allow the sequential flow of the program to de-
termine the order in which the print() function accesses its arguments. You begin by
accessing the author and title information. Then, with each subsequent appearance of the
@ABAlcott array in its scalar form, you retrieve an element from the array. After the poem,
you identify the source. Figure 10.5 illustrates the output of Listing10_05.