```
```java
private boolean isStringArg(char argChar) {
    return stringArgs.containsKey(argChar);
}

private void setBooleanArg(char argChar, boolean value) {
    booleanArgs.put(argChar, value);
}

private boolean isBooleanArg(char argChar) {
    return booleanArgs.containsKey(argChar);
}

public int cardinality() {
    return argsFound.size();
}

public String usage() {
    if (schema.length() > 0)
        return “[-” + schema + “]”;
    else
        return “”;
}

public String errorMessage() throws Exception {
    switch (errorCode) {
        case OK:
            throw new Exception(“TILT: Should not get here.”);
        case UNEXPECTED_ARGUMENT:
            return unexpectedArgumentMessage();
        case MISSING_STRING:
            return String.format(“Could not find string parameter for -%c.”,
                                 errorArgumentId);

        case INVALID_INTEGER:
            return String.format(“Argument -%c expects an integer but was
’%s’.”,
                                 errorArgumentId);
```
```