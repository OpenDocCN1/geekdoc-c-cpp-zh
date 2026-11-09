```
```java
private double doubleValue = 0;

public void set(Iterator<String> currentArgument) throws
ArgsException {
    String parameter = null;
    try {
        parameter = currentArgument.next();
        doubleValue = Double.parseDouble(parameter);
    } catch (NoSuchElementException e) {
        errorCode = ErrorCode.MISSING_DOUBLE;
        throw new ArgsException();
    } catch (NumberFormatException e) {
        errorParameter = parameter;
        errorCode = ErrorCode.INVALID_DOUBLE;
        throw new ArgsException();
    }
}

public Object get() {
    return doubleValue;
}
}
```
```

This forces us to add a new `ErrorCode`.

```
```java
private enum ErrorCode {
    OK, MISSING_STRING, MISSING_INTEGER,
    INVALID_INTEGER, UNEXPECTED_ARGUMENT,
    MISSING_DOUBLE, INVALID_DOUBLE}
```
```

And we need a `getDouble` function.

```
```java
public double getDouble(char arg) {
    Args.ArgumentMarshaller am = marshalers.get(arg);
    try {
        return am == null ? 0 : (Double) am.get();
    } catch (Exception e) {
        return 0.0;
    }
}
```
```