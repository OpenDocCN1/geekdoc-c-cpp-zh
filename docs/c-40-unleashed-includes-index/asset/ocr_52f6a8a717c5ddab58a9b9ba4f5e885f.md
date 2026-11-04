A thorough discussion about satellite assemblies is beyond the scope of this book. In essence, they are resource-only assemblies that get stored in a culture-specific folder right next to the application’s executable assembly. At runtime, when resources are queried for using APIs like `System.Resources`, the framework looks for the most applicable satellite assembly based on the user’s culture and gets the requested resource objects from there.

Localization and globalization are topics that deserve books of their own. For more information, refer to MSDN.

![](bbox=[0.079, 0.283, 0.537, 0.581])

**FIGURE 25.36** An embedded resource’s name as shown through .NET Reflector.

# Type Forwarding

When designing and evolving nontrivial frameworks, it’s often challenging to put types in the right assembly. Although a certain spot may make lots of sense in a certain version of the framework, that doesn’t necessarily remain the case in future releases. For reasons such as architectural layering, it might be a good idea to relocate a type to some other assembly (for example, to avoid the need for excessive references between assemblies).

Such a situation arose in the move from .NET 3.5 to .NET 4. In the former release, generic delegate types such as `System.Func<T, TResult>` were introduced. Because this release of the framework was layered on top of .NET 2.0 baseline assemblies, it was chosen not to touch them for the addition of new types, and the set of Func and Action delegates ended up in a newly crafted `System.Core` assembly. Since things have evolved, those types are used more and more (for example, in the DLR introduced in .NET 4). It no longer made sense for all DLR libraries and users thereof to have to refer to this `System.Core` assembly to use things as trivial as Func and Action delegates. Their new and better home was mscorlib.