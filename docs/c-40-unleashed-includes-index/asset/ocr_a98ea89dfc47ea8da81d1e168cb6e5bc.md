An example of an implementation for one of the property change methods is to reject invalid input by means of throwing an exception. Yet another use is to perform some kind of logging whenever changes happen. What's quintessential about the partial methods feature is that it cleanly separates generated code from customizable code, while both kinds of code belong to the same type definition:

```
partial class Person
{
    partial void OnAgeChanging(int value)
    {
        if (value <= 0)
            throw new ArgumentOutOfRangeException("value");
    }

    partial void OnCreated()
    {
        Console.WriteLine("New Person created.");
    }
}
```

When no implementation is given for a partial method, the whole call site (typically in the generated portion of the class definition) simply disappears. For example, for the preceding code, the setter for Age will really look like this:

```
if ((this._Age != value)) {
    this.OnAgeChanging(value);
    this.SendPropertyChanging();
    this._Age = value;
    this.SendPropertyChanged("Age");
    // This code gets dropped as no implementation is given:
    // this.OnAgeChanged();
}
```

It's easy to verify this claim using tools like Reflector or ILDASM. As a result of this technique, partial methods can only be void-returning and cannot have any output parameters. If that weren't the case, it would be unclear what those resulting output values for the method call would have to be if no implementation is given.

Also, partial methods can only be private (and for that reason no access modifier is allowed). If they were public and someone were to try to call them without having the guarantee an implementation exists, things would go terribly wrong. Along the same lines, it's impossible for a delegate to refer to a partial method because it might not exist.

In summary, the use of partial methods is usually related to code-generation scenarios where the code generator wants to provide “extensibility points” to the developer. By