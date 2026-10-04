considered a friend assembly. You would think that the C# compiler could determine this on its because it normally determines the output file name on its; however, the compiler doesn't decide on an output file name until it is finishing the code. So requiring the /out:<file> compiler switches the performance of compiling significantly.

Also, if you are compiling a module (as opposed to an assembly) using C#'s /:module switch, and this module is going to become part of a friend assembly, you need to compile the module using the C# compiler's /moduleassembly:<string> switch as well. This tells the compiler what assembly the module will be a part of so the compiler can allow code in the module to access the other assembly's internal types.

# Member Accessibility

When defining a member (which includes nested types), you can specify the member's accessibility. A member's accessibility indicates which members can be accessed from referenced code. The CLR defines the set of possible accessibility modifiers, but each programming language chooses the syntax and it wants developers to use when applying the accessibility to a member. For example, the CLR uses the term Assembly to indicate that a member is accessible to any code within the same assembly, whereas the C# term for it is internal.

Table 6-1 shows the six accessibility modifiers that can be applied to a member. The rows of the table are from most restrictive (Private) to least restrictive (Public).

TABLE 6-1 Member Accessibility

| CLR Term | C# Term | Description |
|---|---|---|n| Private | private | The member is accessible only by methods in the defining type or any nested type. |
| Family | protected | The member is accessible only by methods in the defining type, any nested type, or one of its derived types without regard to assembly. |
| Family and Assembly | (not supported) | The member is accessible only by methods in the defining type, any nested type, or by any derived types defined in the same assembly. |
| Assembly | internal | The member is accessible only by methods in the defining assembly. |
| Family or Assembly | protected internal | The member is accessible by any nested type, any derived type (regardless of assembly), or by any methods in the defining assembly. |
| Public | public | The member is accessible to all methods in any assembly. |

Of course, for any member to be accessible, it must be defined in a type that is visible. For example, if AssemblyA defines an internal type with a public method, in AssemblyB cannot call the internal because the internal type is not visible to AssemblyB.