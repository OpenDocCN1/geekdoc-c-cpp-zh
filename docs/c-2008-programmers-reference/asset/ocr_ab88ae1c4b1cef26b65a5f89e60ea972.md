# Access Modifiers

*Access modifiers* are keywords that you can add to members of a class to restrict their access. Consider the following definition of the *Contact* class:

```
```
public class Contact
{
    public const ushort MAX_EMAIL = 5;
    public static int count;
    public int ID;
    public string FirstName;
    public string LastName;
    private string _Email;
}
```
```

Unlike the rest of the data members, the *_Email* data member has been defined with the *private* keyword. The *public* keyword indicates that the data member is visible outside the class, while the *private* keyword indicates that the data member is only visible within the class.

*By convention, you can denote a private variable by beginning its name with the underscore (_) character. This is recommended, but not mandatory.*

For example, you can access the *FirstName* data member through an instance of the *Contact* class:

```
```
//---this is OK---
contact1.FirstName = "Wei-Meng";
```
```

But you cannot access the *_Email* data member outside the class, as the following statement demonstrates:

```
```
//---error: _Email is inaccessible---
contact1._Email = "weimenglee@learn2develop.net";
```
```

*C# has four access modifiers — private, public, protected, and internal. The last two are discussed with inheritance in the next chapter.*

If a data member is declared without the *public* keyword, its scope (or access) is *private* by default. So, *_Email* can also be declared like this:

```
```
public class Contact
{
    public const ushort MAX_EMAIL = 5;
    public static int count;
    public int ID;
    public string FirstName;
    public string LastName;
    string _Email;
}
```
```