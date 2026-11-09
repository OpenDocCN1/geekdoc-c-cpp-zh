+   - **AssemblyVersion** This version number is stored in the AssemblyDef manifest metadata table. The CLR uses this version number when binding to strongly named assemblies (discussed in Chapter 3). This number is extremely important and is used to uniquely identify an assembly. When starting to develop an assembly, you should set the major, minor, build, and revision numbers and shouldn’t change them until you’re ready to begin work on the next deployable version of your assembly. When Assembly-A references a strongly named Assembly-B, Assembly-B’s version is embedded inside Assembly-A’s AssemblyRef table’s entry. This way, when the CLR needs to load Assembly-B, it knows exactly which version Assembly-A was built and tested with. It is possible to have the CLR load a different version by using a binding redirect, which is discussed in Chapter 3.

# ## Culture

Like version numbers, assemblies also have a culture as part of their identity. For example, I could have an assembly that is strictly for German, another assembly for Swiss German, another assembly for US English, and so on. Cultures are identified via a string that contains a primary and a secondary tag (as described in RFC 1766). Table 2-6 shows some examples.

**TABLE 2-6** Examples of Assembly Culture Tags

| Primary Tag | Secondary Tag | Culture |
| --- | --- | --- |
| De | (none) | German |
| De | AT | Austrian German |
| De | CH | Swiss German |
| En | (none) | English |
| En | GB | British English |
| En | US | US English |

In general, if you create an assembly that contains code, you don’t assign a culture to it. This is because code doesn’t usually have any culture-specific assumptions built into it. An assembly that isn’t assigned a culture is referred to as being *culture neutral*.

If you’re designing an application that has some culture-specific resources to it, Microsoft highly recommends that you create one assembly that contains your code and your application’s default (or fallback) resources. When building this assembly, don’t specify a culture. This is the assembly that other assemblies will reference when they create and manipulate types it publicly exposes.

Now you can create one or more separate assemblies that contain only culture-specific resources—no code at all. Assemblies that are marked with a culture are called *satellite assemblies*. For these satellite assemblies, assign a culture that accurately reflects the culture of the resources placed in the assembly. You should create one satellite assembly for each culture you intend to support.