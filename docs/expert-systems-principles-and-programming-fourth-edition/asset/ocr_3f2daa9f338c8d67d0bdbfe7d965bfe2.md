The first example call to string-to-field takes the string field "7.3" and converts it to the integer field value of 7. The second example call to string-to-field has several fields contained in the string argument passed into it. The first field found, the floating-point field 3.4, is returned and the remaining fields in the string are discarded. Note that the extra spacing in the string has no effect on the returned value. Essentially calling string-to-field is identical to calling the read function where the string argument represents what the user types at the keyboard.

# Finding a Symbol

The apropos command can be used to display all symbols defined in CLIPS that contain a specific substring. The syntax of the apropos command is:

```
(apropos <symbol-or-string-expression>)
```

where <symbol-or-string-expression> is the substring being sought. The apropos command is really useful when you want to display a list of functions or commands sharing a common substring or you can remember part but not all of a symbol used in a function, command, or construct. For example, suppose you want a list of all the functions and commands containing the symbol deftemplate:

```
CLIPS> (apropos deftemplate).
get-deftemplate-list
deftemplate
list-deftemplates
undeftemplate
ppdeftemplate
deftemplate-module
CLIPS>
```

# Sorting a List of Fields

The sort function can be used for a list of fields. The syntax of the sort function is:

```
(sort <comparison-function-name> <expression>*)
```

where <comparison-function-name> is the name of the function, deffunction, or generic function that is used to determine whether two fields need to be swapped during sorting. The remaining arguments denoted by <expressions>* can be either single- or multifield values. They are joined together into a single multifield value, which is then sorted. The return value of this function is a sorted multifield value. The following example sorts a list of integers:

```
CLIPS> (sort > 4 3 5 7 2 7).
(2 3 4 5 7 7)
CLIPS>
```