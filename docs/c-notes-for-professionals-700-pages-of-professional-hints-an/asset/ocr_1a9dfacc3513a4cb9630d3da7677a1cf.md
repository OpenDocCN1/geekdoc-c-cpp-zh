# Chapter 24: Guid

GUID (or UUID) is an acronym for 'Globally Unique Identifier' (or 'Universally Unique Identifier'). It is a 128-bit integer number used to identify resources.

# Section 24.1: Getting the string representation of a Guid

A string representation of a Guid can be obtained by using the built in ToString method

```
string myGuidString = myGuid.ToString();
```

Depending on your needs you can also format the Guid, by adding a format type argument to the ToString call.

```
var guid = new Guid("7febf16f-651b-43b0-a5e3-0da8da49e90d");

// None "7febf16f651b43b0a5e30da8da49e90d"
Console.WriteLine(guid.ToString("N"));

// Hyphens "7febf16f-651b-43b0-a5e3-0da8da49e90d"
Console.WriteLine(guid.ToString("D"));

// Braces "{7febf16f-651b-43b0-a5e3-0da8da49e90d}"
Console.WriteLine(guid.ToString("B"));

// Parentheses "(7febf16f-651b-43b0-a5e3-0da8da49e90d)"
Console.WriteLine(guid.ToString("P"));

// Hex "{0x7febf16f, 0x651b, 0x43b0, {0xa5, 0x3, 0x0d, 0xa8, 0xda, 0x49, 0xe9, 0x0d}}"
Console.WriteLine(guid.ToString("X"));
```

# Section 24.2: Creating a Guid

These are the most common ways to create an instance of Guid:

+   - Creating an empty guid (00000000-0000-0000-0000-000000000000):
+   - Creating a new (pseudorandom) Guid:
+   - Creating Guids with a specific value:

```
Guid g = Guid.Empty;
Guid g2 = new Guid();

Guid g = Guid.NewGuid();

Guid g = new Guid("0b214de7-8958-4956-8eed-28f9ba2c47c6");
Guid g2 = new Guid("0b214de7-8958-4956-8eed-28f9ba2c47c6");
Guid g3 = Guid.Parse("0b214de7-8958-4956-8eed-28f9ba2c47c6");
```

# Section 24.3: Declaring a nullable GUID

Like other value types, GUID also has a nullable type which can take null value.

Declaration :

```
Guid? myGuidVar = null;
```