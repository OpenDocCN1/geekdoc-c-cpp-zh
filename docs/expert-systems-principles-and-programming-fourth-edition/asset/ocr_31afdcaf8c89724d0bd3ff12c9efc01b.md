```
CLIPS> (watch message-handlers RECTANGLE
compute-area).]
CLIPS> (watch message-handlers RECTANGLE
get-height primary).]
CLIPS>
```

The first watch command will watch all of the user- and system-defined message-handlers for the CIRCLE class. The second watch command will watch the primary compute-area message-handler for the RECTANGLE class (and it would also watch the after, before, and around handlers if any of these were defined). The third watch command will watch just the primary get-height system-defined message-handler for the RECTANGLE class.

# Defmessage-Handler Commands

Several commands are provided for manipulating defmessage-handlers. The list-defmessage-handlers command is used to display the current list of defmessage-handlers maintained by CLIPS. Its syntax is:

```
(list-defmessage-handlers
 [<defclass-name> [inherit]])
```

where the keyword inherit indicates that you want inherited message-handlers to be listed. For example:

```
CLIPS> (list-defmessage-handlers RECTANGLE).]
get-height primary in class RECTANGLE
put-height primary in class RECTANGLE
get-width primary in class RECTANGLE
put-width primary in class RECTANGLE
compute-area primary in class RECTANGLE
For a total of 5 message-handlers.
CLIPS>
```

The ppdefmessage-handler (pretty print defmessage-handler) command is used to display the text representation of a defmessage-handler. The undefmessage-handler command is used to delete a defmessage-handler. The get-defmessage-handler-list function returns a multifield value containing the list of defmessage-handlers belonging to a specified class. The syntax of these commands is:

```
(ppdefmessage-handler <defclass-name>
 <handler-name>
 [<handler-type>])
(undefmessage-handler <defclass-name>
 <handler-name>
 [<handler-type>])
```