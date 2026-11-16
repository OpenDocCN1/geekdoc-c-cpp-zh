```
CLIPS>
(check-input "Who moves first, Computer or Human?"
c h).]
Who moves first, Computer or Human? (c h) computer.]
Who moves first, Computer or Human? (c h) human.]
Who moves first, Computer or Human? (c h) h]
h
CLIPS>
```

When check-input is called in this example, the string “Who moves first, Computer or Human?” is bound to the parameter ?question. The remaining arguments, c and h, are converted to a multifield value and stored in the wildcard card parameter $?values.

# Defunction Commands

The ppdeffunction (pretty print deffunction) command is used to display the text representations of a deffunction. The undefunction command is used to delete a deffunction. The list-deffunctions command is used to display the list of deffunctions defined in CLIPS. The get-deffunction-list function returns a multifield value containing the list of deffunctions. The syntax of these commands is:

```
(ppdeffunction <deffunction-name>)
(undeffunction <deffunction-name>)
(list-deffunctions [<module-name>])
(get-deffunction-list [<module-name>])
```

The following examples show how to use these functions:

```
CLIPS> (list-deffunctions).]
hypotenuse-length
primep
check-input
factorial
A
B
C
For a total of 7 deffunctions.
CLIPS> (get-deffunction-list).]
(hypotenuse-length primep check-input factorial
A B C)
CLIPS> (undeffunction primep).]
.
```