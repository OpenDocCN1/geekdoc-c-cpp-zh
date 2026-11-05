
## 15.7.2 Static and instance properties

When a property declaration includes a static modifier, the property is said to be a static property. When no static modifier is present, the property is said to be an instance property.

A static property is not associated with a specific instance, and it is a compile-time error to refer to this in the accessors of a static property.

An instance property is associated with a given instance of a class, and that instance can be accessed as this (§12.7.8) in the accessors of that property.

The differences between static and instance members are discussed further in §15.3.8.

## 15.7.3 Accessors

The accessor-declarations of a property specify the executable statements associated with reading and writing that property.

```
accessor-declarations:
    get-accessor-declaration  set-accessor-declarationopt
    set-accessor-declaration  get-accessor-declarationopt

get-accessor-declaration:
    attributesopt accessor-modifieropt get accessor-body

set-accessor-declaration:
    attributesopt accessor-modifieropt set accessor-body

accessor-modifier:
    protected
    internal
    private
    protected internal
    internal protected

accessor-body:
    block
    ;
```

The accessor declarations consist of a get-accessor-declaration, a set-accessor-declaration, or both. Each accessor declaration consists of optional attributes, an optional accessor-modifier, the token get or set, followed by an accessor-body.

The use of accessor-modifiers is governed by the following restrictions:

- An accessor-modifier shall not be used in an interface or in an explicit interface member implementation.
- For a property or indexer that has no override modifier, an accessor-modifier is permitted only if the property or indexer has both a get and set accessor, and then is permitted only on one of those accessors.
- For a property or indexer that includes an override modifier, an accessor shall match the accessor-modifier, if any, of the accessor being overridden.
- The accessor-modifier shall declare an accessibility that is strictly more restrictive than the declared accessibility of the property or indexer itself. To be precise:
  - If the property or indexer has a declared accessibility of public, the accessor-modifier may be either protected internal, internal, protected, or private.
  - If the property or indexer has a declared accessibility of protected internal, the accessor-modifier may be either internal, protected, or private.
  - If the property or indexer has a declared accessibility of internal or protected, the accessor-modifier shall be private.
- If the property or indexer has a declared accessibility of private, no accessor-modifier may be used.

For abstract and extern properties, the accessor-body for each accessor specified is simply a semicolon.

A non-abstract, non-extern property may be an automatically implemented property, in which case both get and set accessors shall be given, both with a semicolon body (§15.7.4). For the accessors of any other non-abstract, non-extern property, the accessor-body is a block that specifies the statements to be executed when the corresponding accessor is invoked.

A get accessor corresponds to a parameterless method with a return value of the property type. Except as the target of an assignment, when a property is referenced in an expression, the get accessor of the property is invoked to compute the value of the property (§12.2.2). The body of a get accessor shall conform to the rules for value-returning methods described in §15.6.11. In particular, all return statements in the body of a get accessor shall specify an expression that is implicitly convertible to the property type. Furthermore, the endpoint of a get accessor shall not be reachable.

A set accessor corresponds to a method with a single value parameter of the property type and a void return type. The implicit parameter of a set accessor is always named value. When a property is referenced as the target of an assignment (§12.18), or as the operand of ++ or -- (§12.7.10, 12.8.6), the set accessor is invoked with an argument that provides the new value (§12.18.2). The body of a set accessor shall conform to the rules for void methods described in §15.6.11. In particular, return statements in the set accessor body are not permitted to specify an expression. Since a set accessor implicitly has a parameter named value, it is a compile-time error for a local variable or constant declaration in a set accessor to have that name.

Based on the presence or absence of the get and set accessors, a property is classified as follows:

- A property that includes both a get accessor and a set accessor is said to be a read-write property.
- A property that has only a get accessor is said to be a read-only property. It is a compile-time error for a read-only property to be the target of an assignment.
- A property that has only a set accessor is said to be a write-only property. Except as the target of an assignment, it is a compile-time error to reference a write-only property in an expression. [Note: The pre- and postfix ++ and -- operators and compound assignment operators cannot be applied to write-only properties, since these operators read the old value of their operand before they write the new one. end note]

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

the Button control declares a public Caption property. The get accessor of the Caption property returns the string stored in the private caption field. The set accessor checks if the new value is different from the current value, and if so, it stores the new value and repaints the control. Properties often follow the pattern shown above: The get accessor simply returns a value stored in a private field, and the set accessor modifies that private field and then performs any additional actions required to update fully the state of the object.

Given the Button class above, the following is an example of use of the Caption property:

```
Button okButton = new Button();  // Invokes set accessor
okButton.Caption = "OK";
string s = okButton.Caption;       // Invokes get accessor
```

Here, the set accessor is invoked by assigning a value to the property, and the get accessor is invoked by referencing the property in an expression. end example]

The get and set accessors of a property are not distinct members, and it is not possible to declare the accessors of a property separately. [Example: The example

```
class A
{
    private string name;
    public string Name {
        get { return name; }      // Error, duplicate member name
    }
    public string Name {
        set { name = value; }     // Error, duplicate member name
    }
}
```

does not declare a single read-write property. Rather, it declares two properties with the same name, one read-only and one write-only. Since two members declared in the same class cannot have the same name, the example causes a compile-time error to occur. end example]

When a derived class declares a property by the same name as an inherited property, the derived property hides the inherited property with respect to both reading and writing. [Example: In the following code

```
class A
{
    public int P {
        set {...}
    }
}
class B: A
{
    new public int P {
        get {...}
    }
}
```

the P property in B hides the P property in A with respect to both reading and writing. Thus, in the statements

```
B b = new B();
b.P = 1;    // Error, B.P is read-only
((A)b).P = 1;   // Ok, reference to A.P
```

the assignment to b.P causes a compile-time error to be reported, since the read-only P property in B hides the write-only P property in A. Note, however, that a cast can be used to access the hidden P property. end example]

Unlike public fields, properties provide a separation between an object's internal state and its public interface. [Example: Consider the following code, which uses a Point struct to represent a location:

```
class Label
{
    private int x, y;
    private string caption;
```
