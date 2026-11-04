# Appendix A: Keywords/Reserved Identifiers

| abstract | decimal | float | namespace | return | try |
|---|---|---|---|---|---|
| as | default | for | new | sbyte | typeof |
| base | delegate | foreach | null | sealed | uint |
| bool | do | goto | object | short | ulong |
| break | double | if | operator | sizeof | unchecked |
| byte | else | implicit | out | stackalloc | unsafe |
| case | enum | in | override | static | ushort |
| catch | event | int | params | string | using |
| char | explicit | interface | private | struct | virtual |
| checked | extern | internal | protected | switch | void |
| class | false | is | public | this | volatile |
| const | finally | lock | readonly | throw | while |
| continue | fixed | long | ref | true |  |

It is important not to intermix reserved identifiers with programmer-generated references. However, if a situation arises where such a naming conflict cannot be avoided, it is possible to disassociate that identifier from the compiler using the @ symbol (see Example A.1).

# Example A.1.

```
using System;
namespace Appendix_A {
    class Class1 {
        [STAThread]
        static void Main(string[] args) {
            int @true = 325;
            string @while = "Salvatore A. Buono";
            Console.WriteLine(@true);
            Console.WriteLine(@while);
        }
    }
}
```