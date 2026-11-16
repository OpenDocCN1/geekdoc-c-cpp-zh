(format <logical-name> <string-expression> <expression>*)
Evaluates and prints as formatted output to the logical name <logical-name> zero or more expressions formatted by <string-expression>. See Section 8.12 for details on formatting flags.

(open <file-name> <logical-name> [<mode>])
Opens the file <file-name> in the specified mode (either "r", "w", "r+", or "a") and associates the logical name <logical-name> with the file. Returns TRUE if the file was successfully opened, otherwise FALSE.

(printout <logical-name> <expression>*)
Evaluates and prints as unformatted output to the logical name <logical-name> zero or more expressions.

(read [<logical-name>])
Reads a single field from the specified logical name (stdin if unspecified). Returns the field if successful or EOF if no input available.

(readline [<logical-name>])
Reads an entire line from the specified logical name (stdin if unspecified). Returns a string if successful or EOF if no input available.

(remove <file-name>)
Deletes the file <file-name>.

(rename <old-file-name> <new-file-name>)
Renames the file <old-file-name> to <new-file-name>.

# Memory

(conserve-mem on | off)
Turns on or off the storage of information used for the save and pretty-print commands.

(mem-used)
Returns the number of bytes of memory CLIPS has requested from the operating system.

(mem-requests)
Returns the number of times CLIPS has requested memory from the operating system.

(release-mem)
Releases all free memory held internally by CLIPS to the operating system. The return value is the amount of memory freed.

# Miscellaneous

(funcall <function-name-expression> <expression>*)
Constructs a function call from its arguments and then evaluates the function call.

(gensym*)
Returns a sequenced symbol of the form genX where X is an integer.

(gensym*)
Returns a sequenced symbol of the form genX where X is an integer. Unlike the gensym function, gensym* produces a unique symbol that does not currently exist within the CLIPS environment.

(get-function-restrictions <function-name-expression>)
Returns the restriction string associated with a CLIPS or user defined function.