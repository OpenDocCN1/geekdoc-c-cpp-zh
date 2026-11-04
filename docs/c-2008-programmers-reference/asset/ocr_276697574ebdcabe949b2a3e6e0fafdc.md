# Part I: C# Fundamentals

Using the same Contact class used in the previous section, add the methods highlighted in the following code:

```
public class Contact
{
    public int ID;
    public string FirstName;
    public string LastName;
    public string Email;

    public override bool Equals(object obj)
    {
        //---check for null obj---
        if (obj == null) return false;

        //---see if obj can be cast to Contact---
        Contact c = obj as Contact;
        if ((System.Object)c == null) return false;

        //---check individual fields---
        return (ID == c.ID) && (FirstName == c.FirstName) &&
            (LastName == c.LastName) && (Email == c.Email);
    }

    public bool Equals(Contact c)
    {
        //---check for null obj---
        if (c == null) return false;

        //---check individual fields---
        return (ID == c.ID) && (FirstName == c.FirstName) &&
            (LastName == c.LastName) && (Email == c.Email);
    }

    public override int GetHashCode()
    {
        return ID;
    }
}
```

Essentially, you're adding the following:

+   - [ ] The Equals(object obj) method to override the Equals() virtual method in the System.Object class. This method takes in a generic object (System.Object) as argument.
+   - [ ] The Equals(Contact c) method to test for value equality. This method is similar to the first method, but it takes in a Contact object as argument.
+   - [ ] The GetHashCode() method to override the GetHashCode() virtual method in the System.Object class.