+   - If the property or indexer has a declared accessibility of private, no accessor-modifier may be used.

For abstract and extern properties, the accessor-body for each accessor specified is simply a semicolon.

A non-abstract, non-extern property may be an automatically implemented property, in which case both get and set accessors shall be given, both with a semicolon body (§15.7.4). For the accessors of any other non-abstract, non-extern property, the accessor-body is a block that specifies the statements to be executed when the corresponding accessor is invoked.

A get accessor corresponds to a parameterless method with a return value of the property type. Except as the target of an assignment, when a property is referenced in an expression, the get accessor of the property is invoked to compute the value of the property (§12.2.2). The body of a get accessor shall conform to the rules for value-returning methods described in §15.6.11. In particular, all return statements in the body of a get accessor shall specify an expression that is implicitly convertible to the property type. Furthermore, the endpoint of a get accessor shall not be reachable.

A set accessor corresponds to a method with a single value parameter of the property type and a void return type. The implicit parameter of a set accessor is always named value. When a property is referenced as the target of an assignment (§12.18), or as the operand of ++ or -- (§12.7.10, 12.8.6), the set accessor is invoked with an argument that provides the new value (§12.18.2). The body of a set accessor shall conform to the rules for void methods described in §15.6.11. In particular, return statements in the set accessor body are not permitted to specify an expression. Since a set accessor implicitly has a parameter named value, it is a compile-time error for a local variable or constant declaration in a set accessor to have that name.

Based on the presence or absence of the get and set accessors, a property is classified as follows:

+   - A property that includes both a get accessor and a set accessor is said to be a read-write property.
+   - A property that has only a get accessor is said to be a read-only property. It is a compile-time error for a read-only property to be the target of an assignment.
+   - A property that has only a set accessor is said to be a write-only property. Except as the target of an assignment, it is a compile-time error to reference a write-only property in an expression. [Note: The pre- and postfix ++ and -- operators and compound assignment operators cannot be applied to write-only properties, since these operators read the old value of their operand before they write the new one. end note]

[Example: In the following code

```
public class Button: Control
{
    private string caption;
    public string Caption {
        get {
            return caption;
        }
        set {
            if (caption != value) {
                caption = value;
                Repaint();
            }
        }
    }
    public override void Paint(Graphics g, Rectangle r) {
    } // Painting code goes here
}
```

the Button control declares a public Caption property. The get accessor of the Caption property returns the string stored in the private caption field. The set accessor checks if the new value is different