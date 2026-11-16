method #2 is now executed, the user enters the value 2, which is in the allowed range, and then both methods return. Generally it's more useful to watch methods instead of generic-functions since you want to know the specific method that's executed, but the option exists to watch either.

# Defmethod Commands

Several commands are provided for manipulating defmethods. The ppdefmethod (pretty print defmethod) command is used to display the text representation of a defmethod. The undefmethod command is used to delete a defmethod. The list-defmethods command is used to display a list of defmethods defined in CLIPS. The get-defmethod-list function returns a multi-field value containing the list of defmethods. The syntax of these commands is:

```
(ppdefmethod <defgeneric-name> <index>)
(undefmethod <defgeneric-name> <index>)
(list-defmethods [<defgeneric-name>])
(get-defmethod-list [<defgeneric-name>])
```

The ppdefmethod and undefmethod commands differ from those of other constructs in that you have to specify an index in addition to the name of the defgeneric. Also the list-defmethods and get-defmethod-list functions do not take an optional module name argument. Instead the optional argument is the name of a generic function. If this is specified, then the command applies only to methods of that generic function; otherwise it is applied to all methods of all generic functions. The following are examples showing the use of these functions:

```
CLIPS> (ppdefmethod check-input 5).]
(defmethod MAIN::check-input
(?question ($?values = (length$ ?values) 0)))
(return FALSE))
CLIPS> (undefmethod check-input 4).]
CLIPS> (list-defmethods).]
check-input #6 (STRING) (INTEGER) (INTEGER <qry>)
check-input #2 (STRING) (INTEGER) (INTEGER)
check-input #7 (STRING) (NUMBER) (NUMBER <qry>)
check-input #3 (STRING) (NUMBER) (NUMBER)
check-input #5 (()) ($? <qry>)
check-input #1 (()) $?
For a total of 6 methods.
CLIPS> (get-defmethod-list check-input).]
(check-input 6 check-input 2 check-input 7
check-input 3 check-input 5 check-input 1)
CLIPS>
```