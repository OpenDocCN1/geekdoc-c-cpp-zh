# # CHAPTER 24
Namespaces

# **IN THIS CHAPTER**

+   ▶ Organizing Types in Namespaces 1213
+   ▶ Declaring Namespaces 1219
+   ▶ Importing Namespaces 1223

While proceeding with our study of the C# programming language and the .NET platform, we've been combining smaller constructs into larger ones. First, we studied what expressions can do for us, followed by a chapter on statements. Next, we grouped those code blocks into members that get organized into types.

Finally, we've arrived at the topmost constructs, which allow for the organization of types into a hierarchical naming scheme and act as containers for deployment. The first is a language construct known as namespaces, also supporting cross-language scenarios. The second is assemblies, which are the CLR's model for code, metadata, and resource containers.

In this chapter, you learn how to organize your types in namespaces and thus avoid name clashes and provide for a logical organization of functionality. Besides declaring namespaces, you also see how to import and use them, including some more tricky scenarios with aliases and extern aliases.

# ## Organizing Types in Namespaces

Simply stated, namespaces provide a way to establish a hierarchical naming scheme for types in .NET libraries and applications. At the language level, it's possible to declare new namespaces containing various types. Besides providing namespaces, there's also the act of using them, which is based on the concept of importing them in code.