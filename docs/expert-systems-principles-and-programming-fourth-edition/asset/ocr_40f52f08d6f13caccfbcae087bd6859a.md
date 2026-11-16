```
(instancep <expression>)
```

Returns TRUE if its argument is an instance name or instance address, otherwise FALSE.

```
(instances [<module-name> [<class-name> {inherit}]])
```

Returns TRUE if its argument is an instance name or instance address, otherwise FALSE.

```
(load-instances <file-name>)
```

Loads instances from the specified file.

```
(make-instance <instance-name> <expression>)
of <class-name-expression> <slot-override>*
<slot-override> ::= (<slot-name-expression>
<expression>)
```

Creates and initializes an instance with the specified slot values.

```
(ppprint)
```

Prints the slots of the active instance when called from within the body of a message-handler.

```
(restore-instances <file-name>)
```

Loads instances from the specified file.

```
(save-instances <file-name>)
```

Saves instances to the specified file.

```
(send <object-expression> <message-name-expression> <expression>*)
```

Sends a message to the specified object with the specified arguments.

```
(slot-delete$ <instance-expression> <mv-slot-name> <range-begin> <range-end>)
```

Allows the deletion of a range of fields in a multifield slot value.

```
(slot-insert$ <instance-expression> <mv-slot-name> <index> <expression>+)
```

Allows the insertion of one or more values in a multifield slot value.

```
(slot-replace$ <instance-expression> <mv-slot-name> <range-begin> <range-end> <expression>+)
```

Allows the replacement of a range of fields in a multifield slot value.

```
(symbol-to-instance-name <symbol-expression>)
```

Converts a symbol to an instance name.

```
(unmake-instance <instance-expression> | *)
```

Deletes the specified instance (or all instances if * is specified) by sending it the delete message.

# I/O

```
(close <logical-name>)
```

Closes the file associated with the logical name <logical-name> (or all files if unspecified). Returns TRUE if the file was successfully closed, otherwise FALSE.