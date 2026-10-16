+   - from
+   - where
+   - select
+   - group
+   - into
+   - orderby
+   - join
+   - let
+   - in
+   - on
+   - equals
+   - by
+   - ascending
+   - descending

These may not be used as identifiers or names but you can use them with the @ prefix. For example, because ‘class’ is a reserved keyword you cannot use it in names or identifiers. However, you can use @class – see the example below:

```
public class @class
{
public static int MyProperty { get; set; }
}
```

```
@class.MyProperty = 100;
```

# What’s Next?