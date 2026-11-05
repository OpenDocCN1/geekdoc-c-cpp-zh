# 13.4.5 Interface Implementation Inheritance

A class inherits all interface implementations provided by its base classes.

> **BILL WAGNER** Eric's earlier comment about "inheritance" being an unfortunate word choice is even more true in this section. Interface methods behave differently than either virtual or non-virtual methods declared in base classes. It can take some time to get your mind around exactly which method is the best choice when multiple classes in a hierarchy declare implementation of an interface. As you read this section, you'll see many different rules for selecting the best method when that method is defined in an interface.

Without explicitly *reimplementing* an interface, a derived class cannot in any way alter the interface mappings it inherits from its base classes. For example, in the declarations

```
interface IControl
{
    void Paint();
}

class Control : IControl
{
    public void Paint() {...}
}

class TextBox : Control
{
    new public void Paint() {...}
}
```

the Paint method in TextBox hides the Paint method in Control, but it does not alter the mapping of Control.Paint onto IControl.Paint, and calls to Paint through class instances and interface instances will have the following effects:

```
Control c = new Control();
TextBox t = new TextBox();
IControl ic = c;
IControl it = t;
c.Paint();    // Invokes Control.Paint();
t.Paint();    // Invokes TextBox.Paint();
ic.Paint();   // Invokes Control.Paint();
it.Paint();   // Invokes Control.Paint();
```