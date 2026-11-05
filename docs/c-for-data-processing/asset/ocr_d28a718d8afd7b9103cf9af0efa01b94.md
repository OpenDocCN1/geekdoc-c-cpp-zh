```
```csharp
private string name;
public string GetName()
{
    return this.name;
}
public static string ValidateName ( string name )
{
    if ( name == null ) {
        return "Name parameter null";
    }
    string trimmedName = name.Trim();
    if ( trimmedName.Length == 0 )
    {
        return "No text in the name";
    }
    return "";
}
public bool SetName ( string inName )
{
    string reply ;
    reply = ValidateName (inName);
    if ( reply.Length > 0 )
    {
        return false;
    }
    this.name = inName.Trim();
    return true;
}
```
```

The name is stored as a private member of the account class. The programmer has provided three methods which let the users of my Account class deal with names. There is a method to get the name, another to set it and another to validate it. The validate method is called by the set method so that my business object makes sure that an account never has an invalid name. The validate method will reject a name string which is empty, or just contains spaces. It trims off all the spaces before and after the name text and then checks to see if the length of the resulting string is empty. If it is, the string is rejected.

I provide the validate method so that users of my class can check their names to make sure that they are valid. This does not involve me in much extra work, since I also use the method myself when validate the name. The validate method returns a string which gives an error message if the string is rejected. There may be several reasons why a name is not valid, at the moment I've given two. The reasons why a name is invalid are of course part of the metadata for the project. I've also made this method static so that names can be validated without needing to have an actual instance of the account.

# Testing Name Handling

Of course, once we have these methods, the natural thing to do is create tests for them: