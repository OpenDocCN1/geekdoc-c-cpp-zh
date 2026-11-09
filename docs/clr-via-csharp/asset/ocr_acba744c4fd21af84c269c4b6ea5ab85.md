```
// internal type as if it were a public type
SomeInternalType sit = new SomeInternalType();
return sit;
}
```

Since the **internal** members of the types in an assembly become accessible to friend assemblies, you should think carefully about what accessibility you specify for your type's members and which assemblies you declare as your friends. Note that the C# compiler requires you to use the **/out:\<file\>** compiler switch when compiling the friend assembly (the assembly that does not contain the **InternalsVisibleTo** attribute). The switch is required because the compiler needs to know the name of the assembly being compiled in order to determine if the resulting assembly should be considered a friend assembly. You would think that the C# compiler could determine this on its own since it normally determines the output file name on its own; however, the compiler doesn't decide on an output file name until it is finished compiling the code. So requiring the **/out:\<file\>** compiler switch improves the performance of compiling significantly.

Also, if you are compiling a module (as opposed to an assembly) using C#'s **/t:module** switch, and this module is going to become part of a friend assembly, you need to compile the module by using the C# compiler's **/moduleassemblyname:\<string\>** switch as well. This tells the compiler what assembly the module will be a part of so the compiler can allow code in the module to access the other assembly's internal types.

> **Important** The friend assembly feature should be used only by assemblies that ship on the same schedule and probably even ship together. The reason is because the interdependency between friend assemblies is so high that shipping the friend assemblies on different schedules will most likely cause compatibility problems. If you expect the assemblies to ship on different schedules, you should try to design **public** classes that can be consumed by any assembly and limit accessibility via a LinkDemand requesting the **StrongNameIdentityPermission**.

# ## Member Accessibility

When defining a type's member (which includes nested types), you can specify the member's accessibility. A member's accessibility indicates which members can be legally accessed from referent code. The CLR defines the set of possible accessibility modifiers, but each programming language chooses the syntax and term it wants developers to use when applying the accessibility to a member. For example, the CLR uses the term Assembly to indicate that a member is accessible to any code within the same assembly, whereas the C# term for this is **internal**.

Table 6-1 shows the six accessibility modifiers that can be applied to a member. The rows of the table are in order from most restrictive (Private) to least restrictive (Public).