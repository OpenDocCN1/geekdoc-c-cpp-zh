```
```java
private boolean booleanValue = false;

public void set(Iterator<String> currentArgument) throws
ArgsException {
    booleanValue = true;
}

public void set(String s) {
    booleanValue = true;
}

public Object get() {
    return booleanValue;
}
}
private class StringArgumentMarshaler extends ArgumentMarshaler {
    private String stringValue = "";

    public void set(Iterator<String> currentArgument) throws
ArgsException {
    }
    public void set(String s) {
        stringValue = s;
    }
    public Object get() {
        return stringValue;
    }
}

private class IntegerArgumentMarshaler extends ArgumentMarshaler {
    private int intValue = 0;

    public void set(Iterator<String> currentArgument) throws
ArgsException {
    }
    public void set(String s) throws ArgsException {
        try {
```
```