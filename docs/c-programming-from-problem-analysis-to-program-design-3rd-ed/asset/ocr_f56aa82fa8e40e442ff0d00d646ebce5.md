4. Tables 2-3 and 2-4 show the keywords in C#. Keywords are predefined reserved identifiers that have special meanings to the compiler. They cannot be used as identifiers in your program. Notice that the keywords in Table 2-4 are identified as “contextual keywords.” Contextual keywords are not as powerful as regular keywords. Contextual keywords have special meaning only when used in a specific situation. Other times they can be used as identifiers.

# Table 2-3 C# keywords/reserved words

| Keywords |  |  |  |  |  |
|---|---|---|---|---|---|
| abstract | as | base | bool | break | byte |
| case | catch | char | checked | class | const |
| continue | decimal | default | delegate | do | double |
| dynamic | else | enum | event | explicit | extern |
| false | finally | fixed | float | for | foreach |
| goto | if | implicit | in | int | interface |
| internal | is | lock | long | namespace | new |
| null | object | operator | out | override | params |
| private | protected | public | readonly | ref | return |
| sbyte | sealed | short | sizeof | stackalloc | static |
| string | struct | switch | this | throw | true |
| try | typeof | uint | ulong | unchecked | unsafe |
| ushort | using | virtual | volatile | void | while |

![](bbox=[0.15, 0.75, 0.2, 0.85])

Contextual keywords only have special meaning when used in a specific context. They were added in an attempt to avoid breaking code that might have been written using earlier standards where one of these words might have been used as a user-defined identifier. For example, yield only has a special meaning when it is used immediately before a return or break statement. Other times, it could be used as an identifier.

# Table 2-4 C# contextual keywords

| Contextual keywords |  |  |  |  |  |
|---|---|---|---|---|---|
| ascending | by | descending | equals | from | get |
| group | in | into | join | let | on |
| orderby | partial | select | set | value | var |
| where | yield |  |  |  |  |