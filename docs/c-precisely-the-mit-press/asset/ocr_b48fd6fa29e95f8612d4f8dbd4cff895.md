# 13.7.4 The Labeled Statement

A labeled statement declares label as the name of a statement; it has the form

```
label : statement
```

where label is an identifier. The scope of label is the entire block enclosing it, including nested blocks. It is illegal to declare the same label twice in a block, including its nested blocks.

# 13.7.5 The goto Statement

A goto statement has one of the forms

```
goto label;
goto case constant;
goto default;
```

The goto case and goto default statements are only allowed inside a switch statement. A goto case constant can target only the cases of the innermost enclosing switch statement (whereas a plain goto may target labels outside; see example a compile-time expression, implicitly convertible to the governing type of the innermost enclosing switch statement.

The effect of a goto statement is that execution continues at the switch label or the clause in the switching statement labeled case constant or default.
The labeled statement must be within the scope of the label. This permits goto to leave a loop or switch but not leave a method or constructor or enter a block or loop or switch.

A goto statement is not allowed to exit a finally block.

See section 13.8.2 for execution of a goto statement inside a try statement that has an associated finally block.

# 13.8 Throwing and Catching Exceptions

# 13.8.1 The throw Statement

A throw statement has one of the forms

```
throw expression;
throw;
```

where the type of expression must be implicitly convertible to class Exception (section 20). A throw statement of the throw expression; is executed as follows. The Expression is evaluated to obtain an exception object v. If it is null, then an instance of NullPointerException is thrown; otherwise the exception object v is thrown. Thus a exception is never null. In any case, the enclosing block is terminated abruptly (section 20). The exception may be caught by a dynamically trying-catch statement: whose exception has begun and not yet completed (section 13.8.2). If the exception is not caught, the entire program execution will be aborted, and information from the exception will be printed at the command prompt or shown in a dialog.

A throw statement of the throw; is only permitted inside the body of a catch statement. Its effect is to rethrow the exception handled by the enclosing catch.

Throwing an exception is slow, so exceptions should not be used for standard control flow.