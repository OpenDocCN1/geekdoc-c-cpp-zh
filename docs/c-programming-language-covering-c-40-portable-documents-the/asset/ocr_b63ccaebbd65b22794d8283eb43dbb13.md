When a class implements multiple interfaces that have the same base interface, there can be only one implementation of the base interface. In the example

```
interface IControl
{
    void Paint();
}
interface ITextBox : IControl
{
    void SetText(string text);
}
interface IListBox : IControl
{
    void SetItems(string[] items);
}
class ComboBox : IControl, ITextBox, IListBox
{
    void IControl.Paint() {...}
    void ITextBox.SetText(string text) {...}
    void IListBox.SetItems(string[] items) {...}
}
```

it is not possible to have separate implementations for the IControl named in the base class list, the IControl inherited by ITextBox, and the IControl inherited by IListBox. Indeed, there is no notion of a separate identity for these interfaces. Rather, the implementations of ITextBox and IListBox share the same implementation of IControl, and ComboBox is simply considered to implement three interfaces: IControl, ITextBox, and IListBox.

The members of a base class participate in interface mapping. In the example

```
interface Interface1
{
    void F();
}
class Class1
{
    public void F() { }
    public void G() { }
}
class Class2 : Class1, Interface1
{
    new public void G() { }
}
```

the method F in Class1 is used in Class2's implementation of Interface1.