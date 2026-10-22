keyword. It’s not available on the method level. Still, it can be used on the class level to define a field that can only be modified during declaration or the execution of the class’s constructor method. So, as soon as the object is available for use, the read-only field will have the same value forever and can’t be modified by the user. Let’s try it out:

```
class SomeClass
{
    private readonly DateTime rightNow;
    public readonly DateTime later =
DateTime.Now.AddHours(2);
    public SomeClass()
    {
    this.rightNow = DateTime.Now;
    }
}
```

So, we have two read-only fields: The first is private, the second one is public (we usually have properties for that, but bear with me here). The first is declared without a value (we can do that with read-only fields, unlike with constants), while the other one is initialized immediately. You will also notice that we’re using the DateTime class as the data type, and we assign a nonconstant value to it. In other words, we do a lot of stuff that we can’t do with constants, making read-only fields an excellent alternative to constants.

Notice how we assign a value to the rightNow field in the constructor of the SomeClass class. As already mentioned, this is the last chance to give a value to a read-only field. After that, whether you are in a method inside the defining class or outside, you will get a compile error if you give a value to a read-only field.