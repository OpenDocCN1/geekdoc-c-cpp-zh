
## Variables and Constants

The simplest definition for a **variable** is that it represents a storage location whose value can change over time. The most common forms of variables are local variables and fields, both of which are defined by providing a type, an identifier, and, optionally, an initial value:

```
int a; int b = 1;
```

If you are declaring multiple variables of the same type, you can combine the declarations, as follows:

```
int a, b;
```

When a variable is declared inside of a limited scope (such as a method), it is said to be a **local variable** and is accessible by name only from within that scope.

> **Scope, Declaration Space, and Lifetime**
> Scope can be thought of as a container in which it is legal to refer to a variable by its unqualified name. This is different from the declaration space, in which no two identifiers are allowed to have the same name. If scope defines where you can use a name, declaration space answers where that name is unique.
>
> The lifetime of a variable is closely connected to its scope and defines how long the variable will be accessible. A variable is guaranteed to be alive at least as long as its scope is executing.
>
> You learn about scope and declaration space in more detail in Hour 3, "Understanding Classes and Objects the C# Way."

A **field** is simply a variable that is not declared inside of a limited scope and can be associated with either the type itself, in which case it is a **static variable** (which you can think of as the equivalent to a global variable), or with an instance of the type, in which case it is an **instance variable**. Local variables and fields must be initialized before they are used and are accessible only while the block containing their declaration is executing.

The code in Listing 1.1 shows a Color type that has private instance fields named red, blue, and green and public static fields named White, Red, Blue, and Green.

### LISTING 1.1 A Color Class

```
class Color
{
    private byte red;
    private byte blue;
    private byte green;

    public Color(byte red, byte blue, byte green)
    {
        this.red = red;
        this.blue = blue;
        this.green = green;
    }

    public static Color White = new Color(0xFF, 0xFF, 0xFF);
    public static Color Red = new Color(0xFF, 0, 0);
    public static Color Blue = new Color(0, 0xFF, 0);
    public static Color Green = new Color(0, 0, 0xFF);
}
```

The static fields are initialized at some point before they are used, but afterward, there is nothing to prevent them from being changed. To accommodate the idea of declaring a field that cannot be changed after it has been assigned, C# enables you to create read-only fields.

> GO TO ▶ Hour 3, for more information on read-only fields.

Listing 1.2 shows the changed lines of the Color class.

### LISTING 1.2 A Color Class Using Read-Only Fields

```
class Color
{
    // ...

    public static readonly Color White = new Color(0xFF, 0xFF, 0xFF);
    public static readonly Color Red = new Color(0xFF, 0, 0);
    public static readonly Color Blue = new Color(0, 0xFF, 0);
    public static readonly Color Green = new Color(0, 0, 0xFF);
}
```

A **constant** represents a value that can be computed at compile time. Constants are associated with the type itself, as if they were static. Like variables, constants can be declared inside of a limited scope or globally. Unlike variables, a constant must always be initialized when it is declared.

## Literal Values and “Magic Numbers”

Literal values are generally numeric values that have special fixed meanings specified directly in code. Over time, the meaning of these literal values can be lost, making that part of the code difficult to maintain. As a result, these literals are often called “magic numbers.” By using constants instead of literal values, the meaning is preserved, making the code self-documenting.

How long would it take you to figure out what the number means in the following function?

```
static float Compute(float f1)
{
    return 299792458 / f1;
}
```

> Did you Know?

Now, if that same function were written using a constant, the meaning of that "magic number" becomes clear:

```
static float Compute(float f1)
{
    const float SpeedOfLight = 299792458;

    return SpeedOfLight / f1;
}
```

In our example, the value 299792458 is a literal value and would therefore be considered a magic number. As you might have guessed, constants are preferred over using just literal values because they have names that can provide more meaning than just a number, and you can guarantee that its value has not changed.

A statement that declares a variable or a constant is generally called a **declaration statement** and can appear anywhere within a block.

## Identifiers and Keywords

When you declare a variable, field, or constant, you must provide both the data type and a meaningful name called an **identifier**.

Identifiers must follow these rules:

-   Only letters (uppercase and lowercase), digits, and the underscore character are valid.
-   An identifier must begin with a letter or the underscore character, although using an underscore (or multiple underscores) as the beginning character for any publicly accessible identifier is considered poor style and should be avoided.
-   Identifiers must be unique within a given declaration space.
-   Identifiers are case-sensitive.

Some additional guidelines that should be followed when choosing identifiers are:

-   Identifiers should be easily readable.
-   Identifiers should not use abbreviations or contractions as part of the name.
-   Identifiers should convey the meaning or intent as much as possible.

In C#, identifiers are case-sensitive. The recommended naming conventions suggest using **camel casing notation**, which capitalizes the first letter of each word except the first word (for example, `bookTitle`) for variable and parameter names and **Pascal casing notation**, which capitalizes the first letter of each word (for example, `BookTitle`) for methods and other identifiers.

### Camel and Pascal Casing

Camel casing is so named because the sequence of letters look like the humps on a camel's back. Pascal casing was named after the style popularized by the Pascal programming language (and because Anders was the original designer of the Turbo Pascal language).

Microsoft no longer recommends using Hungarian notation or using the underscore character to separate words, both common in other languages.

> **Did you know?**
>
> If you are already familiar with another case-sensitive language, such as C, C++, or Java, this should feel normal to you. However, if you are coming from a language that is not case-sensitive, such as Visual Basic, this might take a bit of practice. Fortunately, the Visual Studio 2010 code editor has features that can help make that transition easier.

Because identifiers define the names of specific elements, it is reasonable that the C# language also needs to use identifiers to indicate special meaning to the compiler (and to you), so it has reserved certain identifiers, called **keywords**, for its own uses.

There are 77 keywords in C# reserved at all times under any circumstance; these are listed in Table 1.2.

**TABLE 1.2 C# Keywords**

| abstract | as | base | bool | break |
| :------- | :-- | :--- | :--- | :---- |
| byte | case | catch | char | checked |
| class | const | continue | decimal | default |
| delegate | do | double | else | enum |
| event | explicit | extern | false | finally |
| fixed | float | for | foreach | goto |
| if | implicit | in | int | interface |
| internal | is | lock | long | namespace |
| new | null | object | operator | out |
| override | params | private | protected | public |
| short | sizeof | stackalloc | static | string |
| struct | switch | this | throw | true |
| try | typeof | uint | ulong | unchecked |
| unsafe | ushort | using | virtual | void |
| volatile | while | | | |

An additional 24 keywords, known as **contextual keywords**, have special meaning only in limited circumstances, or context. Outside of that context, these keywords can be for your own purposes, although to minimize confusion, you should try to avoid doing so, if possible. The contextual keywords are listed in Table 1.3.

**TABLE 1.3 Contextual Keywords**

| add | alias | ascending | by | descending |
| :-- | :---- | :-------- | :-- | :--------- |
| dynamic | equals | from | get | global |
| group | into | join | let | on |
| orderby | partial | remove | select | set |
| value | var | where | yield | |

## Visual Studio 2010

Visual Studio is a complete **integrated development environment** (IDE) that is actually made up of many different tools designed with one goal: enabling you to create innovative, next-generation applications. At heart, Visual Studio includes a powerful code editor, language compilers (including support for Visual Basic, C#, C++, and F#), and debugging tools. Visual Studio also includes much more than that:

-   Integration with source control systems
-   Graphical design tools
-   Tools for Microsoft Office, SharePoint, and Cloud development
-   Testing tools

Although it is entirely possible to write applications using your favorite text editor and the command-line utilities that are part of the .NET Framework Software Developer Kit (SDK), it is not practical to do so. The benefits of the integration of the editing and debugging tools, combined with the productivity enhancements provided by Visual Studio, enable you to easily and effectively write and debug your applications.
