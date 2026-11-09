about partial types at all. This is why all of the source code files for the type must use the same programming language, and they must all be compiled together as a single compilation unit.

# Components, Polymorphism, and Versioning

Object-oriented programming (OOP) has been around for many, many years. When it was first used in the late 1970s/early 1980s, applications were much smaller in size and all the code to make the application run was written by one company. Sure, there were operating systems back then and applications did make use of what they could out of those operating systems, but the operating systems offered very few features compared with the operating systems of today.

Today, software is much more complex and users demand that applications offer rich features such as GUIs, menu items, mouse input, tablet input, printer output, networking, and so on. For this reason, our operating systems and development platforms have grown substantially over recent years. Furthermore, it is no longer feasible or even cost effective for application developers to write all of the code necessary for their application to work the way users expect. Today, applications consist of code produced by many different companies. This code is stitched together using an object-oriented paradigm.

Component Software Programming (CSP) is OOP brought to this level. Here are some attributes of a component:

+   - A component (an assembly in .NET) has the feeling of being "published."
+   - A component has an identity (a name, version, culture, and public key).
+   - A component forever maintains its identity (the code in an assembly is never statically linked into another assembly; .NET always uses dynamic linking).
+   - A component clearly indicates the components it depends upon (reference metadata tables).
+   - A component should document its classes and members. C# offers this by allowing in-source Extensible Markup Language (XML) documentation along with the compiler's /doc command-line switch.
+   - A component must specify the security permissions it requires. The CLR's code access security (CAS) facilities enable this.
+   - A component publishes an interface (object model) that won't change for any *servicings*. A *servicing* is a new version of a component whose intention is to be backward compatible with the original version of the component. Typically, a servicing version includes bug fixes, security patches, and possibly some small feature enhancements. But a servicing cannot require any new dependencies or any additional security permissions.