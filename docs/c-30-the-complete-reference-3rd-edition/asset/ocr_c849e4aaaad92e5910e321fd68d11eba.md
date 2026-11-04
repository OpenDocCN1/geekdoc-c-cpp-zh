The following program puts together all of the pieces and demonstrates the use of RemarkAttribute:

```
// A simple attribute example.

using System;
using System.Reflection;

[AttributeUsage(AttributeTargets.All)]
public class RemarkAttribute : Attribute {
    string pri_remark; // underlies Remark property

    public RemarkAttribute(string comment) {
        pri_remark = comment;
    }

    public string Remark {
        get {
            return pri_remark;
        }
    }
}

[RemarkAttribute("This class uses an attribute.")]
class UseAttrib {
    // ...
}

class AttribDemo {
    static void Main() {
        Type t = typeof(UseAttrib);

        Console.Write("Attributes in " + t.Name + ": ");

        object[] attrs = t.GetCustomAttributes(false);
        foreach(object o in attrs) {
            Console.WriteLine(o);
        }

        Console.Write("Remark: ");

        // Retrieve the RemarkAttribute.
        Type tRemAtt = typeof(RemarkAttribute);
        RemarkAttribute ra = (RemarkAttribute)
            Attribute.GetCustomAttribute(t, tRemAtt);

        Console.WriteLine(ra.Remark);
    }
}
```

The output from the program is shown here:

```
Attributes in UseAttrib: RemarkAttribute
Remark: This class uses an attribute.
```