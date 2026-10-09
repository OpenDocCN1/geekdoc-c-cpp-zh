the following attempt to cast a null object raises the
System.NullReferenceException exception:

```
object o2 = null;
try
{
    int i2 = (int)o2;    // Error
}

```

Although the catch clause can be used without arguments to catch any type of
exception, this usage is not recommended. In general, you should only catch those
exceptions that you know how to recover from. Therefore, you should always
specify an object argument derived from System.Exception. For example:

```
catch (InvalidCastException e)
{
}

```

It is possible to use more than one specific catch clause in the same try-catch
statement. In this case, the order of the catch clauses is important because the
catch clauses are examined in order. Catch the more specific exceptions before the
less specific ones. The compiler produces an error if you order your catch blocks so
that a later block can never be reached.

Using catch arguments is one way to filter for the exceptions you want to handle.
You can also use an exception filter that further examines the exception to decide
whether to handle it. If the exception filter returns false, then the search for a
handler continues.

```
catch (ArgumentException e) when (e.ParamName == "...")
{
}

```