For a struct type, within an instance method or instance accessor (§12.2.1) or instance constructor with a constructor initializer, the this keyword behaves exactly as a reference parameter of the struct type (§12.7.8).

# 10.2.7 Output parameters

A parameter declared with an out modifier is an output parameter.

An output parameter does not create a new storage location. Instead, an output parameter represents the same storage location as the variable given as the argument in the function member or delegate invocation. Thus, the value of an output parameter is always the same as the underlying variable.

The following definite assignment rules apply to output parameters. [Note: The rules for reference parameters are different, and are described in §10.2.6. end note]

+   - A variable need not be definitely assigned before it can be passed as an output parameter in a function member or delegate invocation.
+   - Following the normal completion of a function member or delegate invocation, each variable that was passed as an output parameter is considered assigned in that execution path.
+   - Within a function member or anonymous function, an output parameter is considered initially unassigned.
+   - Every output parameter of a function member or anonymous function shall be definitely assigned (§10.4) before the function member or anonymous function returns normally.

Within an instance constructor of a struct type, the this keyword behaves exactly as an output or reference parameter of the struct type, depending on whether the constructor declaration includes a constructor initializer (§12.7.8).

# 10.2.8 Local variables

A local variable is declared by a local-variable-declaration, foreach-statement, or specific-catch-clause of a try-statement. For a foreach-statement, the local variable is an iteration variable (§13.9.5). For a specific-catch-clause, the local variable is an exception variable (§13.11). A local variable declared by a foreach-statement or specific-catch-clause is considered initially assigned.

A local-variable-declaration can occur in a block, a for-statement, a switch-block, or a using-statement.

The lifetime of a local variable is the portion of program execution during which storage is guaranteed to be reserved for it. This lifetime extends from entry into the scope with which it is associated, at least until execution of that scope ends in some way. (Entering an enclosed block, calling a method, or yielding a value from an iterator block suspends, but does not end, execution of the current scope.) If the local variable is captured by an anonymous function (§12.16.6.2), its lifetime extends at least until the delegate or expression tree created from the anonymous function, along with any other objects that come to reference the captured variable, are eligible for garbage collection. If the parent scope is entered recursively or iteratively, a new instance of the local variable is created each time, and its local-variable-initializer, if any, is evaluated each time. [Note: A local variable is instantiated each time its scope is entered. This behavior is visible to user code containing anonymous methods. end note] [Note: The lifetime of an iteration variable (§13.9.5) declared by a foreach-statement is a single iteration of that statement. Each iteration creates a new variable. end note] [Note: The actual lifetime of a local variable is implementation-dependent. For example, a compiler might statically determine that a local variable in a block is only used for a small portion of that block. Using this analysis, the compiler could generate code that results in the variable's storage having a shorter lifetime than its containing block. end note]

The storage referred to by a local reference variable is reclaimed independently of the lifetime of that local reference variable (§8.9). end note

A local variable introduced by a local-variable-declaration is not automatically initialized and thus has no default value. Such a local variable is considered initially unassigned. [Note: A local-variable-declaration