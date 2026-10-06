
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

The goto case and goto default statements are only allowed inside a switch statement. A goto case constant can target only the cases of the innermost enclosing switch statement (whereas a plain goto may target labels outside; see example a). A compile-time expression, implicitly convertible to the governing type of the innermost enclosing switch statement.

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

where the type of expression must be implicitly convertible to class Exception (section 20). A throw statement of the throw expression is executed as follows. The Expression is evaluated to obtain an exception object v. If it is null, then an instance of NullPointerException is thrown; otherwise the exception object v is thrown. Thus a exception is never null. In any case, the enclosing block is terminated abruptly (section 20). The exception may be caught by a dynamically trying-catch statement: whose exception has begun and not yet completed (section 13.8.2). If the exception is not caught, the entire program execution will be aborted, and information from the exception will be printed at the command prompt or shown in a dialog.

A throw statement of the throw; is only permitted inside the body of a catch statement. Its effect is to rethrow the exception handled by the enclosing catch.

Throwing an exception is slow, so exceptions should not be used for standard control flow.

# Example 133 Goto to Exit a Loop

This method uses goto to exit the inner for loop by jumping to the end of the outer loop, thus skipping the first return statement. In more complex examples the use of goto can lead to very unclear code; the use of while as in the equivalent example 126 is often preferable.

```
static bool Substring(String query, String target) {
    for (int j=0; j<target.Length-query.Length; j++) {
        for (int k=0; k<query.Length; k++) {
            if (target[j+k] != query[k])
                goto nextPos;
        }
        return true;
    nextPos:
        // Label on an empty statement
    }
    return false;
}
```

# Example 134 Throwing an Exception to Indicate Failure

Instead of returning the value -1 as in example 130, throw a WeekdayException (example 161).

```
static int WeekdayNo(String wday) {
    for (int i=0; i < wdays.Length; i++) {
        if (wday.Equals(wdays[i]))
            return i+1;
    }
    throw new WeekdayException(wday);
}
```

# Example 135 Implementing a Finite State Machine Using Labeled Statements, goto and switch

This method tests whether str matches the regular expression (a|b)*b: a sequence of a's and b's ending with b. It is a finite state machine with initial state state0 and success state state4.

```
public bool match(String str) {
    int stop = str.Length, i = 0;
    state0:
        if (i==stop) return false;
        switch (str[i++]) {
            case 'a': goto state2;
            case 'b': goto state1;
            default: return false;
        }
    state2: ...
    state3: ...
    state4:
        if (i==stop) return true;
        switch (str[i++]) {
            case 'a': goto state2;
            case 'b': goto state1;
            default: return false;
        }
}
```

# 13.8.2 The try-catch-finally Statement

A try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

```
try
    trybody
    catchclause1;
    catchclause2
    ...
    finally
    finallybody
```

where trybody and finallybody are block statements. There may be zero or more catch clauses, and the finally clause may be absent, but at least one catch or finally clause must be present. No return or break or continue or goto can exit the finallybody. A catchclause must have one of these three forms:

```
catch (exceptiontype identifier)
    catchbody

catch (exceptiontype)
    catchbody

catch
    catchbody
```

where exceptiontype is an Exception or subclass (section 20) and identifier is a variable. The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

where exceptiontype is an Exception or subclass (section 20) and identifier is a variable. The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

where exceptiontype is an Exception or subclass (section 20) and identifier is a variable. The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

 catch- is-- of..

The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

where exceptiontype is an Exception or subclass (section 20) and identifier is a variable. The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

where exceptiontype is an Exception or subclass (section 20) and identifier is a variable. The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

where exceptiontype is an Exception or subclass (section 20) and identifier is a variable. The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

where exceptiontype is an Exception or subclass (section 20) and identifier is a variable. The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

where exceptiontype is an Exception or subclass (section 20) and identifier is a variable. The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

where exceptiontype is an Exception or subclass (section 20) and identifier is a variable. The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

where exceptiontype is an Exception or subclass (section 20) and identifier is a variable. The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

where exceptiontype is an Exception or subclass (section 20) and identifier is a variable. The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The 13.8.2 The try-catch-finally Statement

-where exceptiontype is an Exception or subclass (section 20) and identifier is a variable. The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody. A catchclause must have one of these three forms: The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

--where exceptiontype is an Exception or subclass (section 20) and identifier is a variable. The try-catch-finally statement has this form and is used to catch certain exceptions thrown by trybody.

# Example 136 A try-catch Statement

This example calls the method WeekDayNo(example 134) inside a try-catch statement that catches exceptions of class WeekdayException (example 161) and its base Exception. The second catch clause will be executed if the array args[0] fails because there is line argument; this throws IndexOutOfRangeException, which is a subclass of Exception. If an exception is caught, it is bound to the variable x, and printed by an implicit call (section 7) to the exception's toString method.

```
public static void Main(String[] args) {
  try {
    Console.WriteLine(args[0] + " is weekday number " + WeekDay4(args[0]));
  } catch (WeekdayException x) {
    Console.WriteLine("Weekday problem: " + x);
  } catch (Exception x) {
    Console.WriteLine("Other problem: " + x);
  }
}
```

# Example 137 A try-finally Statement

This method attempts to read three lines from a text file (see section 25.4), each containing a single floating-point number. Regardless of whether anything goes wrong during reading (premature end of file, ill-formed number), the finally clause will close the reader before the method returns. It would do so if the return statement were inside the try block. The same effect may be achieved with the using statement (example 139).

```
static double[] ReadRecord(String filename) {
  BufferedReader reader = new StreamReader(filename);
  double[] res = new double[3];
  try {
    res[0] = double.Parse(reader.ReadLine());
    res[1] = double.Parse(reader.ReadLine());
    res[2] = double.Parse(reader.ReadLine());
  } finally {
    reader.Close();
  }
  return res;
}
```
