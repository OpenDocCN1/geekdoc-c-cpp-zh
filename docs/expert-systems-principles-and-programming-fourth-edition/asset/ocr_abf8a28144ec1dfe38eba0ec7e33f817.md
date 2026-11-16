values of defglobals defined in CLIPS. The get-defglobal-list function returns a multifield value containing the list of defglobals. The syntax of these commands is:

```
(ppdefglobal <defglobal-name>)
(undefglobal <defglobal-name>)
(list-defglobals [<module-name>])
(show-defglobals [<module-name>])
(get-defglobal-list [<module-name>])
```

The <defglobal-name> for the ppdefglobal and undefglobal commands should use the name of the global variable without the beginning and ending * character (for example, x rather than *x*). The following examples use these functions:

```
CLIPS> (ppdefglobal y)
(defglobal MAIN ?*y* = (+ ?*x* 1))
CLIPS> (list-defglobals)
x
Y
For a total of 2 defglobals.
CLIPS> (get-defglobal-list)
(x y)
CLIPS> (show-defglobals)
?*x* = 3
?*y* = 4
CLIPS> (bind ?*y* 5)
5
CLIPS> (show-defglobals)
?*x* = 3
?*y* = 5
CLIPS> (undefglobal y)
CLIPS> (list-defglobals)
x
For a total of 1 defglobal.
CLIPS>
```

# Defglobal Reset Behavior

The value of a defglobal is restored to its original definition value whenever a reset command is issued or when a bind command is used to change the value of the global and a new value is not supplied. For example: