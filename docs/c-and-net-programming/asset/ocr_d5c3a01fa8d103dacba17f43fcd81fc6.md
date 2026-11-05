# 4. Character Literal

+   a. Character literals in C# are enclosed in the single quotes. Like 'a' or 'B'.
+   b. The character literals are immutable and cannot be changed, but the variables that store those values simply denote storage locations.
+   c. Character literal can be a simple single character or an escape sequence.
+   d. **Single character Literals** : A single character Literals contains a single character enclosed within a single quotes(' ').

# Example

```
```
'a',
'8',
';',
' ',
'' etc
```
```

+   e. **Backslash Character Literals** : Escape sequences are the special characters which have some predefined meaning and start with the backslash character. Following table contains the various character escape sequences with their meanings :

| Constant | Meaning(Name) |
| --- | --- |
| '\n' | New-line |
| '\r' | carriage return |
| '\f' | form feed |
| '\t' | horizontal tab |
| '\a' | alert |
| '\b' | back space |
| '\0' | null |
| '\v' | vertical tab |
| '\\' | back slash |
| '\'' | single quote |
| '\"' | Double quote |

Table 2.4.1 Backslash character literals

# Example

```
```csharp
// C# program that uses character literals

using System;

class Program
```
```