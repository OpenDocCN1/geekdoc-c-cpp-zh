```
var defaultTrack = new MusicTrack();

var print = defaultTrack.ToString();
```

Listing 2-12: Initializing reference type fields

The call to ToString causes a null reference exception because the defaultTrack value has been default-initialized. The ToString method calls ToUpper on its Artist and Name properties, whose default-initialized value is null. We need to be alert to any uses of default-initialized references in order to avoid such problems resulting from accessing a null reference. One way to minimize the impact of default-initialized values is by providing our own instance constructors.

# Instance Constructors

An instance constructor, like a method, can have zero or more parameters. Also like methods, constructors can be overloaded, so we can define several constructors for a type, each with a different number of parameters, or parameters of different types. Constructor definitions for classes, structs, records, and record structs have many similarities, but several important differences exist.

In Listing 2-13, we add a constructor for the MusicTrack struct and use the parameter values to initialize the instance's property values. We use the null-coalescing operator ?? to assign an empty string for each property if its corresponding parameter is null.

```
public readonly struct MusicTrack
{
    public MusicTrack(string artist, string name)
    => (Artist, Name) = (artist ?? string.Empty, name ?? string.Empty);

    public string Artist { get; }
    public string Name { get; }

    public override string ToString()
        => $"{Artist.ToUpper()}: {Name.ToUpper()}";
}
```

Listing 2-13: Adding an instance constructor with parameters

By adding a constructor, we no longer have to rely on MusicTrack users setting the properties explicitly, since the initial values for those properties are set in the constructor. We have made those properties get-only—that is, they can be given a value only in the constructor—and made MusicTrack a readonly struct. However, we must still be cautious of using the property values inside the ToString method because instances of any value type can always be default-initialized, regardless of the presence of a user-defined constructor definition. Adding our own constructor for MusicTrack to give meaningful values to the properties isn't sufficient protection against