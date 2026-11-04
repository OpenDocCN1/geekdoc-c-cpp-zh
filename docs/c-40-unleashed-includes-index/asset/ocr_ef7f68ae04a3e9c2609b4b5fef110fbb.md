```
public static FileStream Open(
    string path,
    FileMode mode,
    FileAccess access,
    FileShare share
) { ... }
```

Imagine what it would look like if FileShare were expanded into four Boolean parameters that stand for Read, Write, Delete, and Inheritable, respectively. Use of the method would involve passing four Booleans that have little meaning to the reader. Writing down a series of flags immediately conveys the message to the reader:

```
File.Open("c:\\boot.ini", FileMode.Open, FileAccess.Read,
    FileShare.Read | FileShare.Write);
```

# NAMED PARAMETERS: A VIABLE ALTERNATIVE?

Some readers might object to the statement that an API with a bunch of Boolean parameters is less desirable, in favor of flags enums. Because C# 4.0 now enables you to specify parameters by name, such an API could be defined with default false values for every parameter. The ones to be set could be passed by name:

```
File.Open(..., read: true, write: true);
```

Although this is a great observation, parameter passing is just one place where enums are used. What if your method takes in a set of flags but needs to store those flags somewhere? Do you now declare a whole bunch of fields (each of which will take up 32 bits by themselves, the size of a Boolean)? Also, do you want to pass those flags on to other methods all over the place? Likely, the answer to both questions is no, so you'll agree that flags are a better idea.

# Checking for Flags

So far, we've explored how a flags enum value can be constructed simply by using the bitwise OR operator. What we haven't explained yet is how the receiving end can find out about the flags that are set on a value. Arithmetic-savvy readers will immediately get some ideas about how to check whether a certain bit in a value is set. In essence, what you're going to do is apply a bit mask to perform the check. Figure 11.9 illustrates this.

The bitwise AND operator comes to the rescue to check whether a flag is set. As an example, the following code takes in a FileShare enum and checks whether the Read flag is set. The use of TryParse (and Parse) enables users to specify flags in a comma-separated manner. Try entering things such as Read, Read, Write, and Delete to see the behavior. Because FileShare lives in the System.IO namespace, you'll have to add a using System.IO; directive at the start of the file: