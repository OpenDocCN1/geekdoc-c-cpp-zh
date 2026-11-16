(save <file-name>)
Saves all of the constructs in the CLIPS environment to the file specified by <file-name>.

(set-auto-float-dividend <boolean-expression>)
Enables the auto-float dividend behavior if <boolean-expression> is FALSE, otherwise disables auto-float dividend behavior. The old value of the auto-float dividend behavior is returned.

(set-dynamic-constraint-checking <boolean-expression>)
Disables dynamic constraint checking if <boolean-expression> is FALSE, otherwise enables dynamic constraint checking. The old value of the constraint checking behavior is returned.

(set-static-constraint-checking <boolean-expression>)
Disables static constraint checking if <boolean-expression> is FALSE, otherwise enables static constraint checking. The old value of the constraint checking behavior is returned.

(system <lexeme-expression>*)
Concatenates its arguments together as a string and passes the string as a command to be executed by the operating system.

# Fact

(assert <RHS-pattern>)
Adds one or more facts to the fact list. The fact address of the last fact added is returned.

(assert-string <string-expression>)
Converts a string to a fact and asserts it. The fact address of the newly asserted fact is returned.

(dependencies <fact-index-or-fact-address>)
Lists all the partial matches from which the specified fact receives logical support.

(dependents <fact-index-or-fact-address>)
Lists all facts that receive logical support from the specified fact.

(duplicate <fact-index-or-fact-address> <RHS-slot>*)
Asserts a duplicated copy of a deftemplate fact with one or more slot values changed.

(facts [<module-name>] [<start-integer-expression> [<end-integer-expression> [<max-integer-expression>]]])
Displays the facts in the fact list. If <module-name> is specified, only those facts visible to the specified module are listed, otherwise facts visible to the current module are listed. Facts with fact indexes less than start-integer-expression or greater than <end-integer-expression> are not listed. If <max-integer-expression> is specified, then no more facts than that value will be listed.

(fact-existp <fact-index-or-fact-address>)
Returns TRUE if the fact specified by its fact-index or fact-address argument exists, otherwise FALSE.

(fact-index <fact-address-expression>)
Returns the fact index associated with a fact address.

(fact-relation <fact-address-expression>)
Returns the deftemplate (relation) name associated with the fact.