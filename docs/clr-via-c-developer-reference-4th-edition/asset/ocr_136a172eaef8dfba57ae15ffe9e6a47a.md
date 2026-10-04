```
[DefaultMemberAttribute("Main")
[DebuggerDisplayAttribute("Richter", Name="Jeff", Target=typeof(Program)]
public sealed class Program {
    Conditional("Debug")
    Conditional("Release")
    public void DoSomething() {
    }

    public Program() {
    }

[CLSCompliant(true)]
[STATThread]
public static void Main() {
    // Get the set of attributes applied to this type
    ShowAttributes(typeof(Program));

    // Get the set of methods associated with the type
    MemberInfo[] members = typeof(Program).GetMembers(
        MemberTypes.Constructor | MemberTypes.Method,
        BindingFlags.DeclaredOnly | BindingFlags.Instance |
        BindingFlags.Public | BindingFlags.Static,
        Type.Name, "*");

    foreach (MemberInfo member in members) {
        // Get the set of attributes applied to this member
        ShowAttributes(member);
    }

    private static void ShowAttributes(MemberInfo attributeInfo, Type attributeTarget) {
        IList<CustomAttributeData> attributes =
            CustomAttributeData.GetCustomAttributes(attributeTarget);

        Console.WriteLine("Attributes applied to {0}: {1}",
            attributeTarget.Name, attributes.Count == 0 ? "None" : String.Empty());

        foreach (CustomAttributeData attribute in attributes) {
            Type t = attribute.Constructor.DeclaringType;
            Console.WriteLine("{0}", t.ToString());
            Console.WriteLine("Constructor called={0}", attribute.Constructor);

            IList<CustomAttributeTypedArgument> posArgs = attribute.Constructor.GetArguments();n            Console.WriteLine("Positional arguments passed to constructor: {0}",
                (posArgs.Count == 0 ? "None" : String.Empty));
            foreach (CustomAttributeTypedArgument pa in posArgs) {
                Console.WriteLine("Type={0}, Value={1}", pa.ArgumentType, pa.TypedValue);
            }

            IList<CustomAttributeNamedArgument> namedArgs = attribute.NamedArguments;
            Console.WriteLine("Named arguments set after construction: {0}",
                (namedArgs.Count == 0 ? "None" : String.Empty));
            foreach (CustomAttributeNamedArgument na in namedArgs) {
                Console.WriteLine("Name={0}, Type={1}, Value={2}",
                    na.MemberInfo.Name, na.TypedValue.ArgumentType, na.TypedValue.Value);
            }
        }
    }
}
```

438 PART III Essential Types