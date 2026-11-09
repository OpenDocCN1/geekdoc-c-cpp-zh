```
```java
if (isBooleanSchemaElement(elementTail))
    marshalers.put(elementId, new BooleanArgumentMarshaler());
else if (isStringSchemaElement(elementTail))
    marshalers.put(elementId, new StringArgumentMarshaler());
else if (isIntegerSchemaElement(elementTail)) {
    marshalers.put(elementId, new IntegerArgumentMarshaler());
} else {
    throw new ParseException(String.format(
    “Argument: %c has invalid format: %s.”, elementId, elementTail), 0);
}
}
}
```
```

Okay, so now let’s look at the whole picture again. [Listing 14-12](#) shows the current form of the Args class.

# **Listing 14-12 Args.java (After first refactoring)**

```
```java
package com.objectmentor.utilities.getopts;

import java.text.ParseException;
import java.util.*;

public class Args {
    private String schema;
    private String[] args;
    private boolean valid = true;
    private Set<Character> unexpectedArguments = new
TreeSet<Character>();
    private Map<Character, ArgumentMarshaler> marshalers =
        new HashMap<Character, ArgumentMarshaler>();
    private Set<Character> argsFound = new HashSet<Character>();
    private int currentArgument;
    private char errorArgumentId = '\0';
    private String errorParameter = “TILT”;
    private ErrorCode errorCode = ErrorCode.OK;

    private enum ErrorCode {
```
```