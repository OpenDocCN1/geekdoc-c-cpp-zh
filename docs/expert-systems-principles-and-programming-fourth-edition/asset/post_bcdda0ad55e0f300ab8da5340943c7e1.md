
```
(get-definstances-list [<module-name>])
```

Returns a multifield value containing the list of definstances in the specified module (or in the current module if <module-name> is unspecified).

```
(list-definstances [<module-name>])
```

Lists the definstances in the specified module (or in the current module if <module-name> is unspecified).

```
(ppdefinstances <definstances-name>)
```

Displays the text of the specified definstances.

```
(undefinstances <definstances-name>)
```

Deletes the specified definstances.

## Defmessage-handler

```
(call-next-handler)
```

When called from within a message-handler, calls the next message-handler that is overridden or shadowed by the executing message-handler.

```
(get-defmessage-handler-class <class-name> [inherit])
```

Returns a multifield value containing triples of class names, handler names, and handler types for the specified class. If inherit is specified, then inherited message-handlers are also included in the multifield value.

```
(list-defmessage-handlers [<class-name> [inherit]])
```

Lists the defmessage-handlers for the specified class in the current module. If no class is specified, the message-handlers for all classes in the current module will be listed. If inherit is specified, then inherited message-handlers will also be displayed.

```
(message-handler-existp <class-name> <handler-name> [<handler-type>])
```

```
<handler-type> ::= around | before | primary | after
```

Returns TRUE if the specified message-handler is defined directly (not by inheritance) for the specified class, otherwise FALSE.

```
(next-handlerp)
```

Returns TRUE if there is another message-handler available for execution, otherwise FALSE.

```
(override-next-handler <expression>*)
```

Calls the next shadowed handler and allows the arguments to be changed.

```
(ppdefmessage-handler <class-name> <handler-name> [<handler-type>])
```

```
<handler-type> ::= around | before | primary | after
```

Displays the text of the specified defmessage-handler. If <handler-type> is unspecified, it is assumed to be primary.

```
(preview-send <class-name> <message-name>)
```

Displays the list of the applicable handlers for a message sent to an instance of the specified class.

```
(undefmessage-handler <class-name> <handler-name>
      [<handler-type>])
<handler-type> ::= around | before |
            primary | after
```

Deletes the specified defmessage-handler. If <handler-type> is unspecified, it is assumed to be primary.

## Defmethod

```
(call-next-method)
```

Calls the next shadowed method.

```
(call-specific-method <defgeneric-name> <method-index>
<expression>*)
```

Calls a particular method of a generic function without regards to method precedence.

```
(get-defmethod-list {<defgeneric-name>})
```

Returns a multifield value containing pairs of defgeneric names and methods indices for all methods in the current module. If a defgeneric name is specified, then only methods belonging to that defgeneric will be included in the return value.

```
(get-method-restrictions <defgeneric-name>)
<method-index>
```

Returns a multifield value containing information about the restrictions for the specified method.

```
(list-all-defmethods [<defgeneric-name>])
```

Lists all defmethods in the current module in order of precedence. If a defgeneric name is specified, then only methods belonging to that defgeneric are listed.

```
(next-methodp)
```

If called from a method for a generic function, the function next-methodp will return the symbol TRUE if there is another method shadowed by the current one. Otherwise, the function will return the symbol FALSE.

```
(override-next-method <expression>*)
```

Calls the next shadowed method allowing new arguments to be provided.

```
(ppdefmethod <defgeneric-name> <index>)
```

Displays the text of the defmethod associated with the specified generic function and method index.

```
(preview-generic <generic-function-name>
<expression>*)
```

Lists all applicable methods for a particular generic function call in order of decreasing precedence, but does not execute them.

```
(undefmethod <defgeneric-name> <index>)
```

Deletes the defmethod associated with the specified generic function and method index.

## Defmodule

```
(list-defmodules)
```

Lists all defmodules in the CLIPS environment.

```
(ppdefmodule <defmodule-name>)
```

Displays the text of the specified defmodule.

```
(set-current-module <defmodule-name>)
```

Sets the current module to the specified module and returns the previous current module.

## Defrule

```
(defrule-module <defrule-name>)
```

Returns the module in which the specified defrule is defined.

```
(get-defrule-list [<module-name>])
```

Returns the list of all defrules in the specified module (or in the current module if <module-name> is unspecified).

```
(get-incremental-reset)
```

Returns the current value of the incremental reset behavior.

```
(list-defrules [<module-name>])
```

Lists the defrules in the specified module (or in the current module if <module-name> is unspecified).

```
(matches <defrule-name>)
```

Displays the list of facts and partial matches that match the patterns of the specified rule.

```
(ppdefrule <defrule-name>)
```

Displays the text of the specified defrule.

```
(refresh <defrule-name>)
```

Refreshes the specified defrule. Activations for the rule that have already fired but are still valid are placed on the agenda.

```
(remove-break [<defrule-name>])
```

Removes a breakpoint for the specified rule. If no rule is specified, all breakpoints are removed.

```
(set-break <defrule-name>)
```

Sets a breakpoint for the specified rule. This will cause rule execution to halt before the rule is fired.

```
(set-incremental-reset <boolean-expression>)
```

Sets the incremental reset behavior.

```
(show-breaks [<module-name>])
```

Lists the rules in the specified module that have breakpoints set (or in the current module if <module-name> is unspecified).

```
(undefrule <defrule-name>)
```

Deletes the specified defrule.

## Deftemplate

```
(deftemplate-module <deftemplate-name>)
```

Returns the module in which the specified deftemplate is defined.

```
(get-deftemplate-list [<module-name>])
```

Returns the list of all deftemplates in the specified module (or in the current module if <module-name> is unspecified).

```
(list-deftemplates [<module-name>])
```

Lists the deftemplates in the specified module (or in the current module if `<module-name>` is unspecified).

```
(ppdeftemplate <deftemplate-name>)
```

Displays the text of the specified deftemplate.

```
(undeftemplate <deftemplate-name>)
```

Deletes the specified deftemplate.

## Environment

```
(apropos <lexeme>)
```

Displays all symbols currently defined in the CLIPS environment that contain the specified substring `<lexeme>`.

```
(batch <file-name>)
```

Allows "batch" processing of CLIPS interactive commands by replacing standard input with the contents of the file `<file-name>`. Returns TRUE if the file was successfully executed, otherwise FALSE.

```
(batch* <file-name>)
```

Executes commands from a file. Unlike the `batch` command, evaluates all of the commands in the specified file before returning rather than replacing standard input.

```
(bload <file-name>)
```

Loads a binary image from a file. Returns TRUE if the file was successfully loaded, otherwise FALSE.

```
(bsave <file-name>)
```

Saves a binary image to a file.

```
(clear)
```

Removes all constructs from the CLIPS environment.

```
(exit)
```

Exits from the CLIPS environment.

```
(get-auto-float-dividend)
```

Returns the current value of the auto-float dividend behavior.

```
(get-dynamic-constraint-checking)
```

Returns the current value of the dynamic constraint checking behavior.

```
(get-static-constraint-checking)
```

Returns the current value of the static constraint checking behavior.

```
(load <file-name>)
```

Loads the constructs stored in the file specified by `<file-name>` into the CLIPS environment. Returns TRUE if the file was successfully loaded, otherwise FALSE.

```
(load* <file-name>)
```

Loads the constructs stored in the file specified by `<file-name>` into the CLIPS environment with the displaying informational messages. Returns TRUE if the file was successfully loaded, otherwise FALSE.

```
(options)
```

Lists the settings of CLIPS compiler flags.

```
(reset)
```

Resets the CLIPS environment.
