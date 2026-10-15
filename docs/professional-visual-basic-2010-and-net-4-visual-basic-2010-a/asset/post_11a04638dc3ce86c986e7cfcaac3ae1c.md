
| ATTRIBUTE | DESCRIPTION |
|---|---|
| `Assembly File Version` | This attribute is used to set the version number of the executable files. This and other deployment-related settings are covered in more detail in Chapter 34. |
| `COM Visible` | This attribute is used to indicate whether this assembly should be registered and made available to COM applications. |
| `Guid` | If the assembly is to be exposed as a traditional COM object, then the value of this attribute becomes the ID of the resulting type library. |
| `NeutralResourcesLanguageAttribute` | If specified, provides the default culture to use when the current user’s culture settings aren’t explicitly matched in a localized application. Localization is covered further in Chapter 27. |

## Compiler Settings

When you select the Compile tab of the project properties, you should see a window similar to the one shown in Figure 1-7. One update to Visual Studio 2010 is the return of the Build Configuration settings. In Visual Studio 2008, the Visual Basic Settings for Visual Studio removed these items from the display; and instead, when developers asked to debug their code, a debug version was built and executed, and only if the developer did an explicit build. (Note that if you are using Beta 2, you won’t see these settings restored by default.)

![](img/d99870e80390742f93963da7be0b2e61_37_0.png)

**FIGURE 1-7**

This presented a challenge because this wasn’t the situation for any other set of Visual Studio settings; and Visual Basic developers were sometimes caught-out when sending what they thought was the latest build of their source code. If on their last “build” they were testing a fix and starting the debugger, then they hadn’t rebuilt the release version. Thus, instead of sending a copy of the released version of their application with that last tested fix, they were really sending the last release build made before the fix. The return of these settings means that you, as the developer, have explicit control over the type of executable (release or debug, x64 or x86) that Visual Studio produces.

If you don’t see these drop-downs in your display, you can restore them by selecting Tools ⇨ Options, and then turning on the Advanced compile options. The main reason to restore these options has to do with two key features that are dependent on this setting. The first is Edit and Continue, which provides the capability to make a change in executing code and without restarting, having that change available in your running code while you continue to debug. This is a great tool for simple mistakes that are found during a debug session, and it is only supported for x86 (32-bit) targeted assemblies. This means you must explicitly target x86, as shown in Figure 1-7.

In Visual Studio 2008, the default was to target AnyCPU, but this meant that on a 64-bit developer workstation, Visual Studio was targeting a 64-bit assembly for your debug environment. When working on a 64-bit workstation, you must explicitly target an x86 environment in order to enable both Edit and Continue as well as the other dependency, COM-Interop. The second key feature related to x86 is COM. COM is a 32-bit protocol (as you’ll see in Chapter 28 on COM-Interop, so you are required to target a 32-bit/x86 environment to support COM-Interop.

Aside from your default project file output directory, this page contains several compiler options. The Option Explicit, Option Infer, and Option Strict settings directly affect your variable usage. Each of the following settings can be edited by adding an Option declaration to the top of your source code file. When placed within a source file each of the following settings applies to all of the code entered in that source file, but only to the code in that file:

- **Option Explicit** — This option has not changed from previous versions of Visual Basic. When enabled, it ensures that every variable is explicitly declared. Of course, if you are using Option Strict, then this setting doesn’t matter because the compiler won’t recognize the type of an undeclared variable. To my knowledge, there’s no good reason to ever turn this option off unless you are developing pure dynamic solutions, for which compile time typing is unavailable.

- **Option Strict** — When this option is enabled, the compiler must be able to determine the type of each variable, and if an assignment between two variables requires a type conversion — for example, from Integer to Boolean — then the conversion between the two types must be expressed explicitly.

- **Option Compare** — This option determines whether strings should be compared as binary strings or whether the array of characters should be compared as text. In most cases, leaving this as binary is appropriate. Doing a text comparison requires the system to convert the binary values that are stored internally prior to comparison. However, the advantage of a text-based comparison is that the character “A” is equal to “a” because the comparison is case-insensitive. This enables you to perform comparisons that don’t require an explicit case conversion of the compared strings. In most cases, however, this conversion still occurs, so it’s better to use binary comparison and explicitly convert the case as required.

- **Option Infer** — This option was new in Visual Studio 2008 and, was added due to the requirements of LINQ. When you execute a LINQ statement, you can have returned a data table that may or may not be completely typed in advance. As a result, the types need to be inferred when the command is executed. Thus, instead of a variable that is declared without an explicit type being defined as an object, the compiler and runtime attempt to infer the correct type for this object.

Existing code developed with Visual Studio 2005 is unaware of this concept, so this option will be off by default for any project that is migrated to Visual Studio 2008 or Visual Studio 2010. New projects will have this option turned on, which means that if you cut and paste code from a Visual Studio 2005 project into a Visual Studio 2010 project, or vice versa, you’ll need to be prepared for an error in the pasted code because of changes in how types are inferred.

From the properties page Option Explicit, Option Strict, Option Compare, and Option Infer can be set to either On or Off for your project. Visual Studio 2010 makes it easy for you to customize specific compiler conditions for your entire project. However, as noted, you can also make changes to the individual compiler checks that are set using something like Option Strict.

Notice that as you change your Option Strict settings in particular, the notifications with the top few conditions are automatically updated to reflect the specific requirements of this new setting. Therefore, you can literally create a custom version of the Option Strict settings by turning on and off individual compiler settings for your project. In general, this table lists a set of conditions that relate to programming practices you might want to avoid or prevent, and which you should definitely be aware of. The use of warnings for the majority of these conditions is appropriate, as there are valid reasons why you might want to use or avoid each but might also want to be able to do each.

Basically, these conditions represent possible runtime error conditions that the compiler can’t detect in advance, except to identify that a possibility for that runtime error exists. Selecting a Warning for a setting bypasses that behavior, as the compiler will warn you but allow the code to remain. Conversely, setting a behavior to Error prevents compilation; thus, even if your code might be written to never have a problem, the compiler will prevent it from being used.

An example of why these conditions are noteworthy is the warning of an Instance variable accessing a Shared property. A Shared property is the same across all instances of a class. Thus, if a specific instance of a class is updating a Shared property, then it is appropriate to get a warning to that effect. This action is one that can lead to errors, as new developers sometimes fail to realize that a Shared property value is common across all instances of a class, so if one instance updates the value, then the new value is seen by all other instances. Thus, you can block this dangerous but certainly valid code to prevent errors related to using a Shared property.

As noted earlier, option settings can be specific to each source file. This involves adding a line to the top of the source file to indicate to the compiler the status of that Option. The following lines will override your project’s default setting for the specified options. However, while this can be done on a per-source listing basis, this is not the recommended way to manage these options. For starters, consistently adding this line to each of your source files is time-consuming and potentially open to error:

```
Option Explicit On
Option Compare Text
Option Strict On
Option Infer On
```

Most experienced developers agree that using Option Strict and being forced to recognize when type conversions are occurring is a good thing. Certainly, when developing software that will be deployed in a production environment, anything that can be done to help prevent runtime errors is desirable. However, Option Strict can slow the development of a program because you are forced to explicitly define each conversion that needs to occur. If you are developing a prototype or demo component that has a limited life, you might find this option limiting.

If that were the end of the argument, then many developers would simply turn the option off and forget about it, but Option Strict has a runtime benefit. When type conversions are explicitly identified, the system performs them faster. Implicit conversions require the runtime system to first identify the types involved in a conversion and then obtain the correct handler.

Another advantage of Option Strict is that during implementation, developers are forced to consider every place a conversion might occur. Perhaps the development team didn’t realize that some of the assignment operations resulted in a type conversion. Setting up projects that require explicit conversions means that the resulting code tends to have type consistency to avoid conversions, thus reducing the number of conversions in the final code. The result is not only conversions that run faster, but also, it is hoped, a smaller number of conversions.

Option Infer is a powerful feature. It is used as part of LINQ and the features that support LINQ, but it affects all code. In the past, you needed to write the AS <type> portion of every variable definition in order to have a variable defined with an explicit type. However, now you can dimension a variable and assign it an integer or
