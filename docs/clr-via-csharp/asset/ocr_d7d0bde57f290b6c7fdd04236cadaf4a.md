```
```csharp
using System;
using System.Reflection;
using Microsoft.CSharp.RuntimeBinder;

// This class is used to demonstrate reflection
// It has a field, constructor, method, property, and an event
internal sealed class SomeType {
    private Int32 m_someField;
    public SomeType(ref Int32 x) { x *= 2; }
    public override String ToString() { return m_someField.ToString(); }
    public Int32 SomeProp {
        get { return m_someField; }
        set {
            if (value < 1)
                throw new ArgumentOutOfRangeException("value");
            m_someField = value;
        }
    }
    public event EventHandler SomeEvent;
    private void NoCompilerWarnings() { SomeEvent.ToString(); }
}

public static class Program {
    private const BindingFlags c_bf = BindingFlags.DeclaredOnly | BindingFlags.Public |
        BindingFlags.NonPublic | BindingFlags.Instance;

    public static void Main() {
        Type t = typeof(SomeType);
        UseInvokeMemberToBindAndInvokeTheMember(t);
        Console.WriteLine();

        BindToMemberThenInvokeTheMember(t);
        Console.WriteLine();

        BindToMemberCreateDelegateToMemberThenInvokeTheMember(t);
        Console.WriteLine();

        UseDynamicToBindAndInvokeTheMember(t);
        Console.WriteLine();
    }

    private static void UseInvokeMemberToBindAndInvokeTheMember(Type t) {
        Console.WriteLine("UseInvokeMemberToBindAndInvokeTheMember");

        // Construct an instance of the Type
        Object[] args = new Object[] { 12 };  // Constructor arguments
        Console.WriteLine("x before constructor called: " + args[0]);
        Object obj = t.InvokeMember(null, c_bf | BindingFlags.CreateInstance,
            null, null, args);
        Console.WriteLine("Type: " + obj.GetType().ToString());
        Console.WriteLine("x after constructor returns: " + args[0]);
```
```