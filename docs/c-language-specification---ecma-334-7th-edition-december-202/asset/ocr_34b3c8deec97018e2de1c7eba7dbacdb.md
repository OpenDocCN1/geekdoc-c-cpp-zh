results in the field-targeted attribute NonSerialized being applied to the compiler-generated backing field, as if the code had been written as follows:

```
[Serializable]
public class Foo
{
    [NonSerialized]
    private string _mySecretBackingField;
    public string MySecret
    {
        get { return _mySecretBackingField; }
        set { _mySecretBackingField = value; }
    }
}
```

*end example*

# 15.7.5 Accessibility

If an accessor has an accessor_modifier, the accessibility domain (§7.5.3) of the accessor is determined using the declared accessibility of the accessor_modifier. If an accessor does not have an accessor_modifier, the accessibility domain of the accessor is determined from the declared accessibility of the property or indexer.

The presence of an accessor_modifier never affects member lookup (§12.5) or overload resolution (§12.6.4). The modifiers on the property or indexer always determine which property or indexer is bound to, regardless of the context of the access.

Once a particular non-ref-valued property or non-ref-valued indexer has been selected, the accessibility domains of the specific accessors involved are used to determine if that usage is valid:

+   - If the usage is as a value (§12.2.2), the get accessor shall exist and be accessible.
+   - If the usage is as the target of a simple assignment (§12.21.2), the set accessor shall exist and be accessible.
+   - If the usage is as the target of compound assignment (§12.21.4), or as the target of the ++ or -- operators (§12.8.15, §12.9.6), both the get accessors and the set accessor shall exist and be accessible.

*Example:* In the following example, the property A.Text is hidden by the property B.Text, even in contexts where only the set accessor is called. In contrast, the property B.Count is not accessible to class M, so the accessible property A.Count is used instead.

```
class A
{
    public string Text
    {
        get => "hello";
        set { }
    }

    public int Count
    {
        get => 5;
        set { }
    }
}
```