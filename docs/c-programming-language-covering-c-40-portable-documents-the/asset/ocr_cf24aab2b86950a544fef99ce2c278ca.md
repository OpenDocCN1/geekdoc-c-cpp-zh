```
public static TextReader In {
    get {
        if (reader == null) {
            reader = new StreamReader(Console.OpenStandardInput());
        }
        return reader;
    }
}

public static TextWriter Out {
    get {
        if (writer == null) {
            writer = new StreamWriter(Console.OpenStandardOutput());
        }
        return writer;
    }
}

public static TextWriter Error {
    get {
        if (error == null) {
            error = new StreamWriter(Console.OpenStandardError());
        }
        return error;
    }
}
```

The Console class contains three properties—In, Out, and Error—that represent the standard input, output, and error devices, respectively. By exposing these members as properties, the Console class can delay their initialization until they are actually used. For example, upon first referencing the Out property, as in

`Console.Out.WriteLine("hello, world");`

the underlying TextWriter for the output device is created. But if the application makes no reference to the In and Error properties, then no objects are created for those devices.

# 10.7.3 Automatically Implemented Properties

> JON SKEET An early draft of the C# 3.0 specification referred to these properties as "automatic properties." This name was around for just long enough to stick, and is now much more widely used in the community than the full name.

When a property is specified as an automatically implemented property, a hidden backing field is automatically available for the property, and the accessors are implemented to read from and write to that backing field.