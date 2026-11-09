```
```java
if (m instanceof BooleanArgumentMarshaller)
  setBooleanArg(m);
else if (m instanceof StringArgumentMarshaller)
  setStringArg(m);
else if (m instanceof IntegerArgumentMarshaller)
  setIntArg(m);
else
  return false;
} catch (ArgsException e) {
  valid = false;
  errorArgumentId = argChar;
  throw e;
}
return true;
}
```
```

This change is important because we want to completely eliminate the `if-else` chain. Therefore, we needed to get the error condition out of it.

Now we can start to move the `set` functions. The `setBooleanArg` function is trivial, so we’ll prepare that one first. Our goal is to change the `setBooleanArg` function to simply forward to the `BooleanArgumentMarshaller`.

```
```java
private boolean setArgument(char argChar) throws ArgsException {
  ArgumentMarshaller m = marshallers.get(argChar);
  if (m == null)
    return false;
  try {
    if (m instanceof BooleanArgumentMarshaller)
      setBooleanArg(m, currentArgument);
    else if (m instanceof StringArgumentMarshaller)
      setStringArg(m);
    else if (m instanceof IntegerArgumentMarshaller)
      setIntArg(m);
  } catch (ArgsException e) {
    valid = false;
    errorArgumentId = argChar;
    throw e;
```
```