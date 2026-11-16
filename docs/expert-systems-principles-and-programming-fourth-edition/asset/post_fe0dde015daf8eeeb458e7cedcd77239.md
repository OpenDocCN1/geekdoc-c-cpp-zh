
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

## Fact

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

(fact-slot-names <fact-address-expression>)
Returns the slot names associated with the fact.

(fact-slot-value <fact-address-expression> <slot-name>)
Returns the value of the specified slot from the specified fact.

(get-fact-duplication)
Returns the current value of the fact duplication behavior.

(get-fact-list [<module-name>])
Returns the list of all facts in the specified module (or in the current module if <module-name> is unspecified).

(load-facts <file-name>)
Asserts the facts contained in the file <file-name> in the current module. Returns TRUE if successful, otherwise FALSE.

(modify <fact-index-or-fact-address> <RHS-slot>*)
Changes one or more slot values of a deftemplate fact.

(retract <fact-index-or-fact-address>+)
Removes one or more facts from the fact list.

(save-facts <file-name> [visible | local <deftemplate-name>* ])
Saves the specified facts to the file <file-name>. Returns TRUE if successful, otherwise FALSE.

(set-fact-duplication <boolean-expression>)
Allows identical facts to be asserted if <boolean-expression> is FALSE, otherwise prevents duplicate facts from being added to the fact list. The old value of the duplication behavior is returned.

## Instance

(any-instancep <instance-set-template> <query>)
<instance-set-template> ::=
<instance-set-member-template> ::= (<instance-set-member-template>+)
<single-field-variable> <class-name-expression>+)
<query> ::= <boolean-expression>
Returns TRUE if any instance set is found satisfying the specified query, otherwise FALSE is returned.

(class <object-expression>)
Returns a symbol which is the name of the class of its argument.

(delayed-do-for-all-instances <instance-set-template> <query> <expression>*)
First determines all instance sets satisfying the specified query and then evaluates the specified expressions for each of the satisfying instance sets.

(delete-instance)
Deletes the active instance when called from within the body of a message-handler.

(direct-slot-delete <mv-slot-name> <range-begin> <range-end>)
Allows the deletion of a range of fields in a multifield slot value of the active instance from within a message-handler.

(direct-slot-insert <mv-slot-name> <index> <expression>+)
Allows the insertion of one or more values in a multifield slot value of the active instance from within a message-handler.

(direct-slot-replace <mv-slot-name> <range-begin> <range-end> <expression>+)
Allows the replacement of a range of fields in a multifield slot value of the active instance within a message-handler.

(do-for-instance <instance-set-template> <query> <expression>*)
Evaluates the specified expressions for the first instance set satisfying the specified query.

(do-for-all-instances <instance-set-template> <query> <expression>*)
Evaluates the specified expressions for all instance sets satisfying the specified query.

(dynamic-get <slot-name-expression>)
Returns the value of the specified slot of the active instance.

(dynamic-put <slot-name-expression> <expression>*)
Sets the value of the specified slot of the active instance.

(find-instance <instance-set-template> <query>)
Returns a multifield value containing the first instance set found satisfying the specified query.

(find-all-instances <instance-set-template> <query>)
Returns a multifield value containing the all instance sets found satisfying the specified query.

(init-slots)
Implements the init message-handler attached to the class USER. This function should never be called directly unless an init message-handler is being defined such that the one attached to USER will never be called.

(instance-address <instance-expression>)
Converts an instance to an instance address.

(instance-addressp <expression>)
Returns TRUE if its argument is an instance address, otherwise FALSE.

(instance-existp <instance-expression>)
Returns TRUE if the specified instance exists, otherwise FALSE.

(instance-name <instance-expression>)
Converts an instance address to an instance name.

(instance-namep <expression>)
Returns TRUE if its argument is an instance name, otherwise FALSE.

(instance-name->symbol <instance-name-expression>)
Converts an instance name to a symbol.

(instancep <expression>)
Returns TRUE if its argument is an instance name or instance address, otherwise FALSE.

(instances [<module-name> [<class-name> {inherit}]])
Returns TRUE if its argument is an instance name or instance address, otherwise FALSE.

(load-instances <file-name>)
Loads instances from the specified file.

(make-instance <instance-name> <expression>) of <class-name-expression> <slot-override>*
<slot-override> ::= (<slot-name-expression> <expression>)
Creates and initializes an instance with the specified slot values.

(ppprint)
Prints the slots of the active instance when called from within the body of a message-handler.

(restore-instances <file-name>)
Loads instances from the specified file.

(save-instances <file-name>)
Saves instances to the specified file.

(send <object-expression> <message-name-expression> <expression>*)
Sends a message to the specified object with the specified arguments.

(slot-delete$ <instance-expression> <mv-slot-name> <range-begin> <range-end>)
Allows the deletion of a range of fields in a multifield slot value.

(slot-insert$ <instance-expression> <mv-slot-name> <index> <expression>+)
Allows the insertion of one or more values in a multifield slot value.

(slot-replace$ <instance-expression> <mv-slot-name> <range-begin> <range-end> <expression>+)
Allows the replacement of a range of fields in a multifield slot value.

(symbol-to-instance-name <symbol-expression>)
Converts a symbol to an instance name.

(unmake-instance <instance-expression> | *)
Deletes the specified instance (or all instances if * is specified) by sending it the delete message.

## I/O

(close <logical-name>)
Closes the file associated with the logical name <logical-name> (or all files if unspecified). Returns TRUE if the file was successfully closed, otherwise FALSE.
